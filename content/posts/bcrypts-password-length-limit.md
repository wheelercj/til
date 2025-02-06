+++
title = "Bcrypt's password length limit"
date = 2023-08-10T01:57:33-08:00
lastmod = 2025-02-05T19:46:38-08:00
+++

Using [npm's bcrypt v5.1.0](https://www.npmjs.com/package/bcrypt/v/5.1.0), the maximum possible password length without truncation nor preliminary hashing is 72 ASCII **characters** (not just bytes!) as proven with the below script, which:

1. randomly generates a password of length 73
2. creates truncated password copies of lengths 72 and 71
3. hashes all 3 passwords with the same salt
4. compares the hashes

The result is that the hashes of the 73- and 72-character passwords always match, and those of the 72- and 71-character passwords never match.

```js
const bcrypt = require('bcrypt');

async function testBcrypt() {
    const printableAsciiChars = Array.from(
        Array(95).keys()
    ).map((i) => String.fromCharCode(i + 32)).join("");

    const salt = await bcrypt.genSalt(10);

    let countMatching73And72 = 0;
    let countMatching72And71 = 0;
    const N = 100;
    for (let i = 1; i <= N; i++) {
        // randomly choose a password of length 73
        const password73 = Array.from(
            Array(73).keys()
        ).map(
            () => printableAsciiChars[
                Math.floor(Math.random() * printableAsciiChars.length)
            ]
        ).join("");

        const password72 = password73.slice(0, -1);
        const password71 = password73.slice(0, -2);
        const hash73 = await bcrypt.hash(password73, salt);
        const hash72 = await bcrypt.hash(password72, salt);
        const hash71 = await bcrypt.hash(password71, salt);

        if (hash73 === hash72)
            countMatching73And72++;
        if (hash72 === hash71)
            countMatching72And71++;

        process.stdout.write("\r              \riter " + i + "/" + N);
    }
    process.stdout.write("\r              \r");

    console.log(countMatching73And72, "/", N, "matches between 73 and 72");
    console.log(countMatching72And71, "/", N, "matches between 72 and 71");
}

testBcrypt();
```

There are different implementations of bcrypt that have different capabilities, so this may not apply to any other packages or even other versions of the same package.

Side note: if you're going to make a random password generator for real password use, don't do it this way because it's not cryptographically secure.

## Further reading

- [Does bcrypt have a maximum password length? \| Information Security Stack Exchange](https://security.stackexchange.com/questions/39849/does-bcrypt-have-a-maximum-password-length)
- [Okta Bcrypt incident lessons for designing better APIs \| Hacker News](https://news.ycombinator.com/item?id=42955176)
