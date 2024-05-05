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
