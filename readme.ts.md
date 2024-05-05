## How to type efficiently

### Writing types in d.ts file

Typing in TypeScript syntax is more confortable and efficiency compare to JSDoc. You can define your data types in `.d.ts` file and use `import('./path').Type` to import type then type in JSDoc.

```typescript
// color.d.ts
export interface Rgb {
  red: number;
  green: number;
  blue: number;
}

export interface Rgbs extends Rgb {
  alpha: number;
}

export type Color = Rgb | Rbgs | string;
```

```javascript
// here the equivalent types define in JSDocs syntax
// its much more verbose

/**
 * @typedef {object} Rgb
 * @property {number} red
 * @property {number} green
 * @property {number} blue
 */

/** @typedef {Rgb & { alpha: number }} Rgba */

/** @typedef {Rgb | Rgba | string} Color */
```

```javascript
// color.js import type from color.d.ts
/** @type {import('./color').Color} */
const color = { red: 255, green: 255, blue: 255, alpha: 0.1 };
```

### Don't forget Definitely Typed

You don't need to define every data or function in yourself, even you don't use TypeScript, you still can use the type definition provide by [Definitely Typed](https://www.typescriptlang.org/dt/search?search=).

For example, if you developing a Node.js API application with express.js in JavaScript, don't forget to install `@types/node` and `@types/express`.

```bash
$ npm install -D @types/node @types/express
```

In your js file:

```javascript
/** @type {import('express').RequestHandler} */
const handler = async (req, rep) => {
  // req and rep is now with type
};
```

### Checking by project folder

Instead of manually setup for each file, you can use [jsconfig.json](https://www.typescriptlang.org/docs/handbook/tsconfig-json.html) to setup type checking for your whole project.

You can manually create a `jsonconfig.json` file on the root of the project folder or you can run below command to create a `tsconfig.json` then rename it to `jsonconfig.json`.

```bash
$ npx typescript --init
```

Or you can globally install typescript, then use this command:

```bash
$ npm install -g typescript

$ tsc --init
```

Then, rename `tsconfig.json` to `jsconfig.json`

Open the file, you will see a lot of options, most of them disabled by default.

Don't be scare, all you need to do is just uncomment the "JavaScript Support" options and explicitly specify you source path:

```json
{
  "compilerOptions": {
    "checkJs": true,
    "maxNodeModuleJsDepth": 1
  },
  "input": ["src"]
}
```

Create a JavaScript file under source folder, make a silly mistake, VSCode now give you a warn.

```javascript
/** @type {string} */
const foo = 123; // Error: Type 'number' is not assignable to type 'string'.
```

### Setup commands for type checking

A project can be huge with many files, it is almost impossible to open each files to check whether all of them are type safe. We need a smarter and quicker way.

Under `scripts` property in your `package.json` file, create commands like this:

```json
{
  "scripts": {
    "check": "tsc --project jsconfig.json",
    "check:watch": "tsc --watch --project jsconfig.json"
  }
}
```

Now, you can run `check` command for one time checking and run `check:watch` command for keep rechecking when any file under source path changed.

```javascript
$ npm run check

$ npm run check:watch
```
