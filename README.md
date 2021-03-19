# How to Use "ts-check"

## Summary
This is short "How To" on using the awesome type safety of Typescript in Vanilla JS.
It is an extremely flexible option for adding typing to JS and requires very little setup and no build process.
You basically add a comment to the top of a file to enable checking and then annotate functions, variables, objects and classes as needed.
<br />
<br />

When ts-check is enabled, you also get implicit type checking for anything that VS Code can infer.
<br />
<br />

## Adding to a File
At the top of your js file add the following comment
```js
//@ts-check
```
<br />
<br />

## Adding to your VS Code Settings
Add this to your `settings.json` in vs cod, shortcut via `cmd + ,`
```json
{
  "js/ts.implicitProjectConfig.checkJs": true,
}
```
This will enable ts-check on all your js files by default.
To explicitly opt out of type checking add this to a file:
```js
//@ts-nocheck
```
<br />
<br />

# Annotating

## Variables
Annotate next line:
```js
/** @type {string} */
var myVarAsString = dateFromSomethingFnCall();
```
Annotate inline - note use of parens to wrap expression:
```js
var myVarAsNumber = /** @type {number} */(dateFromSomethingFnCall());
```
### `Variable (Inline) Template`
```js
/** @type {__TYPE__} */
```
```js
/** @type {__TYPE__} */ ()
```
<br />
<br />

## Functions
```js
/**
 * @param {string} a
 * @return {string}
 */
const myFun = (a, b) => {
  // code
  return something();
}
```
Typing `this`
```js
/**
 * @this {MyType}
 * @param {string} a
 * @param {number} b
 * @return {number}
 */
function(a, b) {
  //...code
}

```
### `Function Template`
```js
/**
 * @param {__TYPE__} __NAME__
 * @return {__TYPE__}
 */
```
<br />
<br />

## Interfaces  / Custom Types
To Create an Custom Type
```js
/**
 * @typedef { "NORTH" | "EAST" | "SOUTH" | "WEST" } CompassDirection
 */
```

To Create an Interface
```js
/**
 * @typedef {Object} IAwesomeType
 * @property {string} keyA
 * @property {number} keyB
 * @property {CompassDirection} keyC
 * @property {IMyOtherInterface} keyD
 */
```

### `Interface Template`
```js
/**
 * @typedef {Object} __NAME__
 * @property {__TYPE__} __NAME__
 */
```

## Classes

```js
class CoordinatePoint {
    /**
     * @param {number} x
     * @param {number} y
     */
    constructor(x, y) {
        // ...
    }

    /**
     * @return {number}
     */
    getX() {
        // ...
    }

    /**
     * @return {number}
     */
    getY() {
        // ...
    }

    /**
     * @param {string} str
     * @return {CoordinatePoint}
     */
    static fromString(str) {
        // ...
    }
}
```



## "Import" Types
You can import from typescript or TS type definition files with the following annotation
`IAwesomeType` would be available for use in the current file after doing this.
```js
/**
 * @typedef {import("./to/my/path/file.d.ts").IAwesomeType} IAwesomeType
 */
```
