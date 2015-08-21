# karma-stylusPreprocessor

### Configuration Options
 * `paths`: [`Array`] of paths to folders that should be used for file lookup when using `@import`.
 * `save`: [`Boolean`] Indicates whether result of compilation should be saved in project directory.
 * `compress`: [`Boolean`] Indicates whether css should be compressed or not.
 
### Example configuration

```js
module.exports = {
  frameworks: ['mocha', 'sinon-chai'],
  files: [//..],
  exclude:[//..],
  watch: [//..],
  preprocessors: {
    'app/assets/js/__tests__/**/*.styl': ['stylus']
  },
  //karma-stylusPreprocessor
  stylusPreprocessor: {
    options: {
      paths: ['app/assets/styles/_base/buttron'],
      save: true,
      compress: false
    },
    //Modify path
    transformPath: function(path) {
      path = path.replace(/\.styl$/, '.compiled.css');
      path = path.replace(/\/cases\//g, '/cases/compiled/');
      return path;
    }
  },
  webpack: webpackConfig,
  browserNoActivityTimeout: 100000,
  singleRun: true,
  reporters: ['nyan'],
  colors: true,
  browsers: ['PhantomJS_custom'],
    //custom flags
    customLaunchers: {
      'PhantomJS_custom': {
        base: 'PhantomJS',
        options: {
          windowName: 'my-window',
          settings: {
            webSecurityEnabled: false
          },
        },
        flags: ['--load-images=false'],
        debug: false
      }
    },
    // Have phantomjs exit if a ResourceError is encountered 
    // (useful ifkarma exits without killing phantom)
    phantomjsLauncher: {
      exitOnResourceError: true
    }
};
```
