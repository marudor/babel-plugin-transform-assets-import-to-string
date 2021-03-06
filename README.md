# babel-plugin-transform-assets-import-to-string

> Babel plugin that transforms image assets import and requires to urls / cdn

## Table of Contents

-   [About](#about)
-   [Installation](#installation)
-   [Usage](#usage)
    -   [via babelrc](#via-babelrc)
    -   [via Node API](#via-node-api)

## About

This [babel](https://babeljs.io/) plugin allows you to transform asset files into a string uri, allowing you to point your assets to CDN or other hosts, without needing to run your code through module bundlers.

This helps when doing _isomorphic_ / server-rendered applications.

```js
import image from '../path/assets/icon.svg';
const image1 = require('../path/assets/icon1.svg');

// to

const image = 'http://your.cdn.address/assets/icon.svg';
const image1 = 'http://your.cdn.address/assets/icon1.svg';

// Somewhere further down in your code:
//
// eg: JSX
// <img src={image} alt='' />
//
// eg: Other cases
// ajaxAsyncRequest(image)
```

See the spec for more [examples](https://github.com/joblift/babel-plugin-transform-assets-import-to-string/blob/master/test/index.spec.js).

## Installation

```
$> npm install @joblift/babel-plugin-transform-assets-import-to-string --save
```

## Usage

### via .babelrc

```json
{
    "plugins": [
        [
            "@joblift/babel-plugin-transform-assets-import-to-string",
            {
                "baseDir": "/assets",
                "baseUri": "http://your.cdn.address"
            }
        ]
    ]
}
```

### via Node API

```js
require('babel-core').transform('code', {
    plugins: [
        [
            '@joblift/babel-plugin-transform-assets-import-to-string',
            {
                baseDir: '/assets',
                baseUri: 'http://your.cdn.address',
            },
        ],
    ],
});
```

### Configure extensions

By default, it will transform the following extensions: `.gif, .jpeg, .jpg, .png, .svg` if `extensions` option is not defined. To configure a custom list, just add the `extensions` array as an option.

**Note:** leading `.` (dot) is required.

```json
{
    "plugins": [
        [
            "@joblift/babel-plugin-transform-assets-import-to-string",
            {
                "extensions": [".jpg", ".png"]
            }
        ]
    ]
}
```

### Override baseUri during runtime

It supports overriding the baseUri from `process.env`. The name of the env can be set by using the envName property (default is ASSET_BASE_URI).

```json
{
    "plugins": [
        [
            "@joblift/babel-plugin-transform-assets-import-to-string",
            {
                "envName": "FOO_BAR"
            }
        ]
    ]
}
```

If `process.env.FOO_BAR` is set in runtime, it will be used as baseUri.


## License

`@joblift/babel-plugin-babel-plugin-transform-assets-import-to-string` is [MIT licensed](./LICENSE)
