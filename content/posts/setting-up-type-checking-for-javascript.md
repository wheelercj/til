+++
title = 'Setting up type checking for JavaScript'
date = 2025-03-10T13:20:57-07:00
+++

1. `npm install typescript --save-dev` installs TypeScript locally
2. `npx tsc --init --allowJs --checkJs --noEmit` creates tsconfig.json
3. Add `"check-types": "npx tsc"` to the `scripts` object in package.json
4. Run `npm run check-types` to check types

Type annocations can be written with [JSDoc](https://jsdoc.app/) syntax. I often refer to [Jsdoc cheatsheet](https://devhints.io/jsdoc).

## Further reading

- [TypeScript: Documentation - What is a tsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html)
- [TypeScript: Documentation - JS Projects Utilizing TypeScript](https://www.typescriptlang.org/docs/handbook/intro-to-js-ts.html)
- [TypeScript: Documentation - Type Checking JavaScript Files](https://www.typescriptlang.org/docs/handbook/type-checking-javascript-files.html)
- [TypeScript: TSConfig Reference - Docs on every TSConfig option](https://www.typescriptlang.org/tsconfig/)
