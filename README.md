# workspace-alias

Forked from [lerna-alias](https://github.com/Andarist/lerna-alias).

Simple package for getting alias object for packages managed by npm or yarn workspaces, so other tools (such as [webpack](https://webpack.js.org/), [rollup](https://rollupjs.org/), [jest](http://facebook.github.io/jest/) and possibly more) can consume your packages directly from the source files, instead of the built and prepared distribution files.

It just eases development and setting up scripts depending on other monorepo packages.

## API

```js
workspaceAliases({
  // from which directory monorepo should be searched for
  directory: string = process.cwd(),
  // optional array of `mainFields` that should be used to resolv package's entry point
  // similar to the https://webpack.js.org/configuration/resolve/#resolve-mainfields
  // using this takes precedence over default `sourceDirectory` option
  mainFields?: string[],
  // which directory should be considered as containing source files of a package
  // if specified as false it will use package's root and rely on a tool's (i.e. webpack) resolving algorithm
  sourceDirectory: string | false = 'src'
}): Aliases
```

## Types

**Aliases**

```js
type Aliases = {
  // value is a local directory path to the package
  // resolved using `sourceDirectory` and `mainFields` options
  [packageName: string]: string,
}
```

## Usage

## with webpack

```js
const { webpack: workspaceAliases } = require('workspace-alias')

module.exports = {
  // ...
  resolve: {
    // ...
    alias: workspaceAliases(),
  },
}
```

## with Rollup

```js
const { rollup: workspaceAliases } = require('workspace-alias')
const workspaceAliases = require('workspace-alias')

module.exports = {
  // ...
  plugins: [
    // ...
    alias(workspaceAliases()),
  ],
}
```

## with Jest

```js
const { jest: workspaceAliases } = require('workspace-alias')

module.exports = {
  // ...
  moduleNameMapper: workspaceAliases(),
}
```

## using `mainFields` option

```js
const { jest: workspaceAliases } = require('workspace-alias')

module.exports = {
  // ...
  moduleNameMapper: workspaceAliases({ mainFields: ['main'] }),
}
```
