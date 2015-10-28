# svg-url-loader
[![NPM version][npm-version-image]][npm-url] [![NPM downloads][npm-downloads-image]][npm-url] [![MIT License][license-image]][license-url] [![Build Status][travis-image]][travis-url]

Converts SVG file to utf-8 encoded data-uri string.

Existing [`url-loader`](https://github.com/webpack/url-loader) always does Base64 encoding for data-uri.  As SVG content is a human-readable xml string, using base64 encoding is not mandatory.  Instead, one may only escape [unsafe characters](http://www.ietf.org/rfc/rfc1738.txt) and replace `"` with `'` as described [in this article](http://codepen.io/Tigt/post/optimizing-svgs-in-data-uris).  

There are some benefits for choosing utf-8 encoding over base64.  
1. Resulting string is shorter (can be ~2 times shorter for 2K-sized icons);  
2. Resulting string will be compressed better when using gzip compression;  
3. Browser parses utf-8 encoded string faster than its base64 equivalent.


## Usage

[Documentation: Using loaders](http://webpack.github.io/docs/using-loaders.html)

### In JS:
``` javascript
require("svg-url!./file.svg");
// => DataUrl for file.svg, enclosed in quotes

require("svg-url?noquotes!./file.svg");
// => DataUrl for file.svg, without quotes
```

### In CSS (with webpack.config.js below):
``` css
.icon {
    background: url('../images/file.svg');
}
```
``` javascript
module.exports = {
  //...
	module: {
		loaders: [
			{test: /\.svg/, loader: 'svg-url-loader'}
		]
	},
	//...
};
```

## License

MIT (http://www.opensource.org/licenses/mit-license.php)


[license-image]: http://img.shields.io/badge/license-MIT-blue.svg?style=flat
[license-url]: LICENSE

[npm-url]: https://www.npmjs.org/package/svg-url-loader
[npm-version-image]: https://img.shields.io/npm/v/svg-url-loader.svg?style=flat
[npm-downloads-image]: https://img.shields.io/npm/dm/svg-url-loader.svg?style=flat

[travis-url]: https://travis-ci.org/bhovhannes/svg-url-loader
[travis-image]: https://img.shields.io/travis/bhovhannes/svg-url-loader.svg?style=flat
