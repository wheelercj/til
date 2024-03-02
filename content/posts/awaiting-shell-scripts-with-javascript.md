+++
title = 'Awaiting shell scripts with JavaScript'
date = 2024-03-01T23:16:12-08:00
+++

Sometimes it's helpful to await the execution of a shell script using JavaScript, such as when building a web API to automate tasks for which shell scripts are ideal.

I found [an answer by Ansikt and kano on Stack Overflow](https://stackoverflow.com/a/50335035) for how to do this, but discovered some important details in testing that their answer is missing. Here's my version of how to await a shell script:

```js
const { promisify } = require('util');
const promisedExec = promisify(require('child_process').exec);

/**
 * exec executes a command and either returns its output or throws an error. In Windows,
 * only Command Prompt commands can be used with this function.
 * @example
 * try {
 *     const stdout = await exec('echo hello');
 *     console.log(stdout.trim());
 * } catch (error) {
 *     console.log(error.stdout.trim());
 *     console.error(error.stderr.trim());
 * }
 * @param {String} command - the command to be executed.
 * @returns {Promise<String>} - the command's output to stdout.
 * @throws {Object} - an error object with keys `code`, `killed`, `signal`, `cmd`,
 * `stdout`, and `stderr`.
 */
async function exec(command) {
    const output = await promisedExec(command);
    // `output.stderr` never contains the content of stderr.
    return output.stdout;
}

async function main() {
    try {
        const stdout = await exec('echo hello && fake_command');
        console.log(stdout.trim());
    } catch (error) {
        console.log(error.stdout.trim());
        console.error(error.stderr.trim());
    }
}

main();
```

The above code gives this output in Ubuntu:

```shell
hello
/bin/sh: 1: fake_command: not found
```

Here's the output in PowerShell:

```shell
hello
'fake_command' is not recognized as an internal or external command,
operable program or batch file.
```

This uses Node's [`util.promisify`](https://nodejs.org/api/util.html#util_util_promisify_original) and [`child_process`](https://nodejs.org/api/child_process.html); no third-party dependencies.

`child_process` also has a function called `execSync`, which is "a synchronous version of `child_process.exec()` that will block the Node.js event loop." That might sound like a more simple version of using `child_process.exec()` with `util.promisify` like above, but it's not. `await` does not block the event loop, and it's often important to not block the event loop.

## using HTTP status codes . . . kind of

Many shell scripts use an exit code of 1 for every possible error, and 0 for every possible success. Assigning different exit codes to different errors and successes can make a system using the script more robust.

For example, shell scripts can use something like [HTTP status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status) to communicate in a reliable way with more detail. However, Bash does not allow exit codes greater than 255 as explained in [Bash command line exit codes demystified](https://www.redhat.com/sysadmin/exit-codes-demystified) by Ken Hess. One solution is to use two-digit exit codes that are similar to the most commonly used HTTP status codes.

```js
const { promisify } = require('util');
const promisedExec = promisify(require('child_process').exec);

/**
 * execHttpCoded executes a command and returns an object containing the command's
 * output. This function expects the command to only use exit codes that resemble HTTP
 * status codes. Since Bash forbids exit codes greater than 255, this function allows
 * exit codes within the range 10-59 that could have meanings such as:
 * * 20 - success
 * * 21 - created
 * * 24 - no content
 * * 40 - bad request
 * * 41 - unauthorized
 * * 43 - forbidden
 * * 44 - not found
 * * 46 - not acceptable
 * * 49 - conflict
 * * 50 - internal error
 * * 53 - unavailable
 *
 * An exit code of 50 is returned if the command's exit code is outside the range 10-59.
 * In Windows, only Command Prompt commands can be used with this function.
 * @example
 * const res = await execHttpCoded('./my_command.sh arg1 arg2');
 * if (res.code < 30) {
 *     console.log('Success!');
 *     console.log(res.stdout.trim());
 * } else {
 *     console.error(res.stderr.trim());
 * }
 * @param {String} command - the command to be executed.
 * @returns {Promise<Object>} - an object with keys `code`, `killed`, `signal`, `cmd`,
 * `stdout`, and `stderr`.
 */
async function execHttpCoded(command) {
    try {
        const output = await promisedExec(command);
        return {
            code: 50,
            killed: false,
            signal: null,
            cmd: command,
            stdout: output.stdout,
            stderr: "Error: unexpected exit code: 0",
            // `output.stderr` does not contain the content of stderr.
        };
    } catch (res) {
        if (res.code < 10 || res.code > 59) {
            res.stderr = `${res.stderr}\nError: unexpected exit code: ${res.code}`;
            res.code = 50;
        }
        return res;
    }
}
```
