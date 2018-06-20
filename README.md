# eslint-import-resolver-locals-alias

[![Version npm][version]](http://browsenpm.org/package/eslint-import-resolver-locals-alias)
[![Build Status][build]](https://travis-ci.org/johvin/eslint-import-resolver-locals-alias)
[![Download][download]](https://www.npmjs.com/package/eslint-import-resolver-locals-alias)
[![Dependencies][david]](https://david-dm.org/johvin/eslint-import-resolver-locals-alias)
[![Coverage Status][cover]](https://coveralls.io/github/johvin/eslint-import-resolver-locals-alias?branch=master)
[![Known Vulnerabilities][vulnerabilities]](https://snyk.io/test/npm/eslint-import-resolver-locals-alias)
[![License][license]](https://opensource.org/licenses/MIT)

[version]: http://img.shields.io/npm/v/eslint-import-resolver-locals-alias.svg?style=flat-square
[build]: http://img.shields.io/travis/johvin/eslint-import-resolver-locals-alias/master.svg?style=flat-square
[download]: https://img.shields.io/npm/dm/eslint-import-resolver-locals-alias.svg?style=flat-square
[david]: https://img.shields.io/david/johvin/eslint-import-resolver-locals-alias.svg?style=flat-square
[cover]: http://img.shields.io/coveralls/johvin/eslint-import-resolver-locals-alias/master.svg?style=flat-square
[vulnerabilities]: https://snyk.io/test/npm/eslint-import-resolver-locals-alias/badge.svg?style=flat-square
[license]: https://img.shields.io/badge/License-MIT-brightgreen.svg?style=flat-square


This is a simple Node.js module import resolution plugin for [`eslint-plugin-import`](https://www.npmjs.com/package/eslint-plugin-import), which supports native Node.js module resolution, module alias and custom file extensions. Also supports aliases for project modules.


## Installation

Prerequisites: Node.js >=4.x and corresponding version of npm.

```shell
npm install eslint-plugin-import eslint-import-resolver-locals-alias --save-dev
```


## Usage

Pass this resolver and its parameters to `eslint-plugin-import` using your `eslint` config file, `.eslintrc` or `.eslintrc.js`.

```js
// .eslintrc.js
module.exports = {
  settings: {
    'import/resolver': {
      alias: {
        map: [
          ['babel-polyfill', 'babel-polyfill/dist/polyfill.min.js'],
          ['helper', './utils/helper'],
          ['material-ui/DatePicker', '../custom/DatePicker'],
          ['material-ui', 'material-ui-ie10'],
          ['@project-module', 'module/path/'],
          ['project-module2', 'module2']
        ],
        extensions: ['.ts', '.js', '.jsx', '.json']
      }
    }
  }
};
```

Note:

- The alias config object contains two properties, `map` and `extensions`, both of which are array types
- The item of `map` array is also array type which contains 2 string
    + The first string represents the mapped module name or path
    + The second string represents the module alias, the actual module path or name
- The `map` item `['helper', './utils/helper']` means that the module `helper/*` will be resolved to `./utils/helper/*`. See [#3](https://github.com/johvin/eslint-import-resolver-locals-alias/issues/3)
- The order of 'material-ui/DatePicker' and 'material-ui' cannot be reversed, otherwise the alias rule 'material-ui/DatePicker' does not work
- The default value of `extensions` property is `['.js', '.json', '.node']` if it is assigned to an empty array or not specified.

*If the `extensions` property is not specified, the config object can be simplified to the `map` array.*

```js
// .eslintrc.js
module.exports = {
  settings: {
    'import/resolver': {
      alias: [
        ['babel-polyfill', 'babel-polyfill/dist/polyfill.min.js'],
        ['helper', './utils/helper'],
        ['material-ui/DatePicker', '../custom/DatePicker'],
        ['material-ui', 'material-ui-ie10'],
        ['@project-module', 'module/path/'],
        ['project-module2', 'module2']
      ]
    }
  }
};
```

When the config is not a valid object (such as `true`), the resolver falls back to native Node.js module resolution.

```js
// .eslintrc.js
module.exports = {
  settings: {
    'import/resolver': {
      alias: true
    }
  }
};
```

## CHANGELOG

[`CHANGELOG`](./CHANGELOG.md)

## References

- eslint-plugin-import/no-extraneous-dependencies
- eslint-plugin-import/no-unresolved
- eslint-module-utils/resolve
- resolve
- eslint-import-resolver-node

Forked from https://github.com/johvin/eslint-import-resolver-alias