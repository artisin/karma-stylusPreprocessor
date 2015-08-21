# karma-stylusPreprocessor

### Configuration Options
 * `save`: [`Boolean`] Indicates whether result of compilation should be saved in project directory.
 * `paths`: [`Array`] of paths to folders that should be used for file lookup when using `@import`.
 * `compress`: [`Boolean`] Indicates whether css should be compressed or not.
 
### Example configuration

```js
module.exports = {
  frameworks: ['mocha', 'sinon-chai'],
  files: [
    config.sourceAssets + '/js/__tests__/**/*.js',
    config.sourceAssets + '/js/__tests__/**/*.styl',
    config.sourceAssets + '/js/__tests__/**/*.css',
  ],
  exclude:[
    config.sourceAssets + '/js/__tests__/**/*.txt',
  ],
  watch: [//Watch for txt desc to run test],
  preprocessors: {
    'app/assets/js/__tests__/*': ['webpack', 'sourcemap'],
    'app/assets/js/__tests__/**/*.styl': ['stylus']
  },
  //karma-stylusPreprocessor
  stylusPreprocessor: {
    options: {
      paths: ['app/assets/styles/_base/buttron'],
      save: true
    },
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
