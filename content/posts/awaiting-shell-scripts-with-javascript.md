+++
title = 'Awaiting shell scripts with JavaScript'
date = 2024-02-29T12:08:52-08:00
+++

Sometimes it's helpful to await the execution of a shell script using JavaScript, such as when building a web API to automate tasks for which shell scripts are ideal.

I found [an answer by Ansikt and kano on Stack Overflow](https://stackoverflow.com/questions/12941083/execute-and-get-the-output-of-a-shell-command-in-node-js) for how to do this, but discovered some important details in testing that their answer is missing. Here's my version of how to await a shell script:

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
