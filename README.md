# DTRT WordPress Plugin Bump

[![GitHub release](https://img.shields.io/github/release/dotherightthing/gulp-wpdtrt-plugin-bump.svg?branch=master)](https://github.com/dotherightthing/gulp-wpdtrt-plugin-bump/releases) [![Build Status](https://travis-ci.org/dotherightthing/gulp-wpdtrt-plugin-bump.svg?branch=master)](https://travis-ci.org/dotherightthing/gulp-wpdtrt-plugin-bump) [![GitHub issues](https://img.shields.io/github/issues/dotherightthing/gulp-wpdtrt-plugin-bump.svg)](https://github.com/dotherightthing/gulp-wpdtrt-plugin-bump/issues) [![GitHub wiki](https://img.shields.io/badge/documentation-wiki-lightgrey.svg)](https://github.com/dotherightthing/wpdtrt-plugin-boilerplate/wiki)

A Gulp utility to update a fixed selection of files in either the [DTRT WordPress Plugin Boilerplate](https://github.com/dotherightthing/wpdtrt-plugin-boilerplate/), or a child generated with the [DTRT WordPress Plugin Boilerplate Generator](https://github.com/dotherightthing/generator-wp-plugin-boilerplate), using the version information in `package.json`.

## Installation

```sh
npm install https://github.com/dotherightthing/gulp-wpdtrt-plugin-bump --save-dev
```

## Usage

See `wpdtrt-plugin-boilerplate`:

* [`replaceVersions()` - gulp-modules/version.js](https://github.com/dotherightthing/wpdtrt-plugin-boilerplate/blob/9e46fda31099d5aa5d8d169a8a4e33471c18959c/gulp-modules/version.js#L47-L69)
* [`boilerplatePath()` - gulp-modules/boilerplate-path.js](https://github.com/dotherightthing/wpdtrt-plugin-boilerplate/blob/master/gulp-modules/boilerplate-path.js)

## Maintenance

### Pre-requisites

1. Download and install [Mono](https://www.mono-project.com/download/stable/), which is required by [Natural Docs](https://www.naturaldocs.org/).

### Scripts

1. `npm install` - Install NPM dependencies
1. `npm run build` - Run the following scripts:
   1. `npm run dependencies` - Install documentation dependencies
   1. `npm run docs` - Generate documentation to `docs/`
   1. `npm run images` - Optimise images
   1. `npm run lint` - Lint code
   1. `npm run release` - Package release (Travis only)
   1. `npm run tests` - Test code

### Files

1. `./index.js` - Node module, plugins consume this via Gulp tasks, versioned files are output to the specified output folder (for testing this is `tmp/`)
1. `./test/tests.js` - unit tests, written in mocha/chai
1. `./test/fixtures` - plugin files with placeholder version information
1. `./text/fixtures/wpdtrt-generated-plugin/package.json` sets the target `version`
1. `./text/fixtures/wpdtrt-plugin-boilerplate/package.json` sets the target `version`
1. `./test/expected` - plugin files with real version information

#### To add a new file

1. Add the file to the appropriate `fixtures` folders, with a version of `0.12.345`
1. Add the file to the `pluginFilesBoilerplate` and `pluginFilesGeneratedPlugin` arrays in `test/index.js`
1. Add a new regex replacement function to `./index.js`

### Tests

The unit tests confirm that:

1. The script successfully transforms the `fixtures` to their `expected` copies,
   1. When `gulp-wpdtrt-plugin-bump` is run on `wpdtrt-plugin-boilerplate` directly
   1. When `gulp-wpdtrt-plugin-bump` is run on `wpdtrt-generated-plugin` (with a `wpdtrt-plugin-boilerplate` dependency)
   1. When `gulp-wpdtrt-plugin-bump` is run on `wpdtrt-test` (generated by `wpdtrt-plugin-boilerplate`)

### Releases

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
