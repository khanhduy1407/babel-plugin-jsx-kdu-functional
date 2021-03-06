# JSX Functional Components for Kdu JSX

This babel plugin adds some syntactic sugar to JSX.

## Usage:

```bash
npm i babel-plugin-jsx-kdu-functional -D
```
or
```bash
yarn add babel-plugin-jsx-kdu-functional -D
```

Then add `jsx-kdu-functional` to your `.babelrc` file under `plugins`

example .babelrc:
```json
{
  "presets": ["es2015"],
  "plugins": ["jsx-kdu-functional", "transform-kdu-jsx"]
}
```

Example:
```js
const A = () => <h1>Hello World</h1>
export const B = ({ props, listeners }) => <div onClick={listeners.click}>{props.msg}<A /></div>
```
will be transpiled into:
```js
const A = {
  functional: true,
  render: (h) => <h1>Hello World</h1>
}

export const B = {
  functional: true,
  render: (h, { props, listeners }) => <div onClick={listeners.click}>{props.msg}<A /></div>
}
```

### Warning

This plugin will transform **all** named arrow functions that contain JSX and
starting with version 2.0.0 so this code will not work:
```js
const A = () => <h1>Hello World</h1>
export const B = ({ props, listeners }) => <div onClick={listeners.click}>{props.msg}{A()}</div>
```
