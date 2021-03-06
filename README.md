# write-file-webpack-plugin

[![NPM version](http://img.shields.io/npm/v/write-file-webpack-plugin.svg?style=flat-square)](https://www.npmjs.com/package/write-file-webpack-plugin)
[![js-canonical-style](https://img.shields.io/badge/code%20style-canonical-blue.svg?style=flat-square)](https://github.com/gajus/canonical)

Forces `webpack-dev-server` program to write bundle files to the file system.

This plugin has no effect when `webpack` program is used.

## Install

```sh
npm install write-file-webpack-plugin --save-dev
```

## API

```js
/**
 * @typedef {Object} options
 * @property {RegExp} test A regular expression used to test if file should be written. When not present, all bundle will be written.
 * @property {boolean} useHashIndex Use hash index to write only files that have changed since the last iteration (default: true).
 * @property {boolean} log Logs names of the files that are being written (or skipped because they have not changed) (default: true).
 */

/**
 * @param {options} options
 * @returns {Object}
 */
new WriteFilePlugin();

new WriteFilePlugin({
    // Write only files that have ".css" extension.
    test: /\.css$/,
    useHashIndex: true
});
```

## Usage

Configure [`webpack.config.js`](https://webpack.github.io/docs/configuration.html) to use the `write-file-webpack-plugin` plugin.

You must add `outputPath` property to the `devServer` configuration (For explanation see https://github.com/gajus/write-file-webpack-plugin/issues/1). `devServer.outputPath` value must be equal to `output.path` configuration value.

```js
import path from 'path';
import WriteFilePlugin from 'write-file-webpack-plugin';

export default {
    devServer: {
        outputPath: path.join(__dirname, './dist')
    },
    output: {
        path: path.join(__dirname, './dist')
    },
    plugins: [
        new WriteFilePlugin()
    ],
    // ...
}
```

See [./sandbox](./sandbox) for a working `webpack` configuration.
