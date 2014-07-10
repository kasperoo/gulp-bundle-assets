# [gulp](http://gulpjs.com/)-bundle-assets [![NPM version][npm-image]][npm-url] [![Build Status][travis-image]][travis-url]

> Creates asset (js, css) bundles out of a config file

## Install

```shell
npm install gulp-bundle-assets --save-dev
```

## Usage

Create the following files:

```js
// gulpfile.js
var gulp = require('gulp'),
  bundle = require('gulp-bundle-assets');

gulp.task('bundle', function() {
  return gulp.src('./bundle.config.js')
    .pipe(bundle());
});
```

```js
// bundle.config.js
module.exports = {
  bundle: {
    main: {
      js: [
        './content/js/foo.js',
        './content/js/baz.js'
      ],
      css: './content/**/*.css',
      resources: './content/**/*.{png,svg}'
    },
    vendor: {
      js: './bower_components/angular/angular.js'
    }
  }
};
```

Then, calling

```shell
$ gulp bundle
```

Results in the following folder structure:

```
-- public
   |-- content
   |   |-- fonts
   |   |-- images
   `main-bundle.css
   `main-bundle.js
   `vendor-bundle.js
```

see `/examples` for more detail

## Options

### dest

Type: `string`
Default: `./public`

Output destination of bundled assets, e.g.

```js
gulp.task('bundle', function() {
  return gulp.src('./bundle.config.js')
    .pipe(bundler({
      dest: './my/custom/output/path'
    }));
});
```

### base

Type: `string`
Default: `.`

Base directory when resolving src globs. Useful when running gulp tasks from a gulpfile outside the project's root.

## Use your bundles

You can programmatically render your bundles into your view via 
[your favorite templating engine](https://www.google.com/webhp?ion=1&espv=2&ie=UTF-8#q=node%20js%20templating%20engine)
and the resulting `bundle.result.json` file. 
[See here for an example using hogan](examples/express-app-using-result-json/readme.md)

[npm-url]: https://npmjs.org/package/gulp-bundle-assets
[npm-image]: http://img.shields.io/npm/v/gulp-bundle-assets.svg
[travis-image]: https://travis-ci.org/chmontgomery/gulp-bundle-assets.svg?branch=master
[travis-url]: https://travis-ci.org/chmontgomery/gulp-bundle-assets