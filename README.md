# DTRT WordPress Plugin Bump

[![GitHub release](https://img.shields.io/github/release/dotherightthing/gulp-wpdtrt-plugin-bump.svg?branch=master)](https://github.com/dotherightthing/gulp-wpdtrt-plugin-bump/releases) [![Build Status](https://travis-ci.org/dotherightthing/gulp-wpdtrt-plugin-bump.svg?branch=master)](https://travis-ci.org/dotherightthing/gulp-wpdtrt-plugin-bump) [![GitHub issues](https://img.shields.io/github/issues/dotherightthing/gulp-wpdtrt-plugin-bump.svg)](https://github.com/dotherightthing/gulp-wpdtrt-plugin-bump/issues) [![GitHub wiki](https://img.shields.io/badge/documentation-wiki-lightgrey.svg)](https://github.com/dotherightthing/wpdtrt-plugin-boilerplate/wiki)

A Gulp utility to update a fixed selection of files in either the [DTRT WordPress Plugin Boilerplate](https://github.com/dotherightthing/wpdtrt-plugin-boilerplate/), or a child generated with the [DTRT WordPress Plugin Boilerplate Generator](https://github.com/dotherightthing/generator-wp-plugin-boilerplate), using the version information in `package.json`.

## Installation

```sh
yarn add https://github.com/dotherightthing/gulp-wpdtrt-plugin-bump --dev
```

## Usage

As used in [wpdtrt-plugin-boilerplate's gulpfile.js](https://github.com/dotherightthing/wpdtrt-plugin-boilerplate/blob/master/gulpfile.js):

```node
/* globals gulp, taskheader */

var pluginName = process.cwd().split( '/' ).pop();
var wpdtrtPluginBump = require( 'gulp-wpdtrt-plugin-bump' );

gulp.task( 'bump_replace', () => {
  // if run from wpdtrt-plugin-boilerplate:
  // gulp bump
  var inputPathRoot = '';
  var inputPathBoilerplate = '';

  taskheader(
    'Version',
    'Bump',
    'Replace version strings'
  );

  // if run from a child plugin:
  // gulp bump
  // --gulpfile ./vendor/dotherightthing/wpdtrt-plugin-boilerplate/gulpfile.js --cwd ./
  if ( pluginName !== 'wpdtrt-plugin-boilerplate' ) {
    inputPathRoot = '';
    inputPathBoilerplate = 'vendor/dotherightthing/wpdtrt-plugin-boilerplate/';
  }

  return wpdtrtPluginBump( {
    inputPathRoot: inputPathRoot,
    inputPathBoilerplate: inputPathBoilerplate
  } );
} );
```

## Maintenance

### Pre-requisites

1. Download and install [Mono](https://www.mono-project.com/download/stable/), which is required by [Natural Docs](https://www.naturaldocs.org/).

### Scripts

1. `yarn run build` - Install Yarn dependencies, then run the following scripts:
1. `yarn run dependencies` - Install documentation dependencies
1. `yarn run docs` - Generate documentation to <docs/>
1. `yarn run images` - Optimise images
1. `yarn run lint` - Run code linting
1. `yarn run release` - Package release (Travis only)
1. `yarn run tests` - Run unit tests

### Files

1. `./index.js` - Node module, plugins consume this via Gulp tasks, versioned files are output to the specified output folder (for testing this is `tmp/`)
1. `./test/index.js` - unit tests, written in mocha/chai
1. `./test/fixtures` - plugin files with placeholder version information
1. `./text/fixtures/wpdtrt-generated-plugin/package.json` sets the target `version`
1. `./text/fixtures/wpdtrt-plugin-boilerplate/package.json` sets the target `version`
1. `./test/expected` - plugin files with real version information

#### To add a new file:

1. Add the file to the appropriate `fixtures` folders, with a version of `0.12.345`
1. Add the file to the `pluginFilesBoilerplate` and `pluginFilesGeneratedPlugin` arrays in `test/index.js`
1. Add a new regex replacement function to `./index.js`

### Tests

The unit tests confirm that:

1. The script successfully transforms the `fixtures` to their `expected` copies,
  1. When `gulp-wpdtrt-plugin-bump` is run on `wpdtrt-plugin-boilerplate` directly
  1. When `gulp-wpdtrt-plugin-bump` is run on `wpdtrt-generated-plugin` (with a `wpdtrt-plugin-boilerplate` dependency)
  1. When `gulp-wpdtrt-plugin-bump` is run on `wpdtrt-test` (generated by `wpdtrt-plugin-boilerplate`)

### Release

Prior to committing, please update the version number in the following files:

1. `./package.json`
1. `./config/naturaldocs/Project.txt`

## Handy reference links

* [Mocha: Getting Started](https://mochajs.org/#getting-started)
* [A guide to mocha's describe(), it() and setup hooks](https://samwize.com/2014/02/08/a-guide-to-mochas-describe-it-and-setup-hooks/)
* [Chai Assertion Library: BDD - Expect & Should](https://www.chaijs.com/api/bdd/)
* [RegExr: Learn, Build, & Test RegEx](https://regexr.com)
* <https://artandlogic.com/2014/05/a-simple-gulp-plugin/>
* <https://duske.me/simple-functional-tests-for-gulp-tasks/>
* <https://github.com/stevelacy/gulp-bump/blob/master/test/index.js>
* <https://github.com/lazd/gulp-replace/blob/master/test/main.js>
* <https://gulpjs.org/writing-a-plugin/testing>

---

## Technologies

[![node.js](readme-styles/icons/optimised/nodejs.svg)](https://nodejs.org/)
[![Mocha](readme-styles/icons/optimised/mocha.svg)](https://mochajs.org/)
