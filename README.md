[![NPM version](http://img.shields.io/npm/v/webpack-glob.svg?style=flat-square)](https://www.npmjs.org/package/webpack-glob) [![Travis build status](http://img.shields.io/travis/mdreizin/webpack-glob/es6.svg?style=flat-square)](https://travis-ci.org/mdreizin/webpack-glob) [![AppVeyor build status](https://img.shields.io/appveyor/ci/mdreizin/webpack-glob/es6.svg?style=flat-square)](https://ci.appveyor.com/project/mdreizin/webpack-glob/branch/es6) [![Code Climate GPA](https://img.shields.io/codeclimate/github/github/mdreizin/webpack-glob.svg?style=flat-square)](https://codeclimate.com/github/mdreizin/webpack-glob) [![Code Climate Coverage](https://img.shields.io/codeclimate/coverage/github/github/mdreizin/webpack-glob.svg?style=flat-square)](https://codeclimate.com/github/mdreizin/webpack-glob) [![Dependency Status](https://img.shields.io/david/mdreizin/webpack-glob.svg?style=flat-square)](https://david-dm.org/mdreizin/webpack-glob) [![Development Dependency Status](https://img.shields.io/david/dev/mdreizin/webpack-glob.svg?style=flat-square)](https://david-dm.org/mdreizin/webpack-glob#info=devDependencies)

webpack-cluster
===============

Helps to make parallel webpack compilation easily

<h2 id="usage">Usage</h2>

<h3 id="usage-cli">CLI</h3>

```
$ webpack-glob --config=**/webpack.config.js [options]

Compiler:
  --config      Specifies configuration files using `minimatch` pattern
                                                             [string] [required]
  --progress    Displays compilation progress                          [boolean]
  --json        Saves `stats` object to JSON file                      [boolean]
  --silent      Suppress all output                                    [boolean]
  --watch       Runs webpack compiler in `watch` mode                  [boolean]
  --memoryFs    Compiles to memory                                     [boolean]
  --maxWorkers  Number of concurrent workers
                                 [number] [default: require('os').cpus().length]

Webpack:
  --profile  Captures timing information for each module               [boolean]
  --[*]      Many configuration options are mapped from CLI automatically

Miscellaneous:
  --version  Outputs the version number                                [boolean]

```

<h3 id="usage-gulp-js">Gulp.js</h3>

```javascript
import gulp from 'gulp';
import gutil from 'gulp-util';
import CompilerAdapter from 'webpack-glob';

const WEBPACK_OPTIONS = {
        output: {
            path: './dist'
        },
        stats: {
            colors: true,   
            hash: true,
            timings: true,
            chunks: false,
            chunkModules: false,
            modules: false,
            children: true,
            version: false,
            cached: false,
            cachedAssets: false,
            reasons: false,
            source: false,
            errorDetails: false
        }
    },
    COMPILER_OPTIONS = {
        progress: false,
        json: false,
        memoryFs: false
    },
    compilerAdapter = new CompilerAdapter(COMPILER_OPTIONS, WEBPACK_OPTIONS);

gulp.task('run', [], callback => {
    compilerAdapter.run('./src/**/webpack.config.js').then(callback).catch(err => {
        callback(new gutil.PluginError('webpack', err));
    });
});

gulp.task('watch', [], callback => {
    compilerAdapter.watch('./src/**/webpack.config.js').then(callback).catch(err => {
        callback(new gutil.PluginError('webpack', err));
    });
});

```
