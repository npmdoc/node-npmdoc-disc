# npmdoc-disc

#### basic api documentation for  [disc (v1.3.2)](https://github.com/hughsk/disc)  [![npm package](https://img.shields.io/npm/v/npmdoc-disc.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-disc) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-disc.svg)](https://travis-ci.org/npmdoc/node-npmdoc-disc)

#### A tool for analyzing the module tree of a browserify bundle or node project

[![NPM](https://nodei.co/npm/disc.png?downloads=true&downloadRank=true&stars=true)](https://www.npmjs.com/package/disc)

- [https://npmdoc.github.io/node-npmdoc-disc/build/apidoc.html](https://npmdoc.github.io/node-npmdoc-disc/build/apidoc.html)

[![apidoc](https://npmdoc.github.io/node-npmdoc-disc/build/screenCapture.buildCi.browser.%252Ftmp%252Fbuild%252Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-disc/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-disc/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-disc/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Hugh Kennedy",
        "url": "http://hughskennedy.com/"
    },
    "bin": {
        "discify": "bin/discify"
    },
    "bugs": {
        "url": "https://github.com/hughsk/disc/issues"
    },
    "dependencies": {
        "bl": "^0.7.0",
        "browser-unpack": "^0.2.3",
        "builtins": "0.0.3",
        "commondir": "0.0.1",
        "d3": "^3.4.3",
        "duplexer": "^0.1.1",
        "file-tree": "^1.0.0",
        "flatten": "0.0.1",
        "map-async": "^0.1.1",
        "opener": "^1.3.0",
        "optimist": "^0.6.1",
        "plucker": "0.0.0",
        "through": "^2.3.4",
        "uniq": "^1.0.0"
    },
    "description": "A tool for analyzing the module tree of a browserify bundle or node project",
    "devDependencies": {
        "autoprefixer": "^1.1.20140319",
        "browserify": "^3.33.0",
        "btoa": "^1.1.1",
        "clean-css": "^2.1.6",
        "domready": "^1.0.4",
        "marked": "^0.3.2",
        "prettysize": "0.0.3",
        "rework": "^0.20.2",
        "tap-spec": "^2.1.2",
        "tape": "^3.0.3",
        "uglify-js": "^2.4.15"
    },
    "directories": {},
    "dist": {
        "shasum": "32a6f02e486edf77860a5363d22718425d296e40",
        "tarball": "https://registry.npmjs.org/disc/-/disc-1.3.2.tgz"
    },
    "gitHead": "ae3bfb34f7c29d3f469a2ac4e28247d5f4021dca",
    "homepage": "https://github.com/hughsk/disc",
    "keywords": [
        "analyze",
        "analytics",
        "directory",
        "file",
        "modules",
        "tree",
        "tool",
        "browserify",
        "size",
        "structure",
        "visualize"
    ],
    "license": "MIT",
    "main": "index.js",
    "maintainers": [
        {
            "name": "hughsk"
        }
    ],
    "name": "disc",
    "optionalDependencies": {},
    "repository": {
        "type": "git",
        "url": "git://github.com/hughsk/disc.git"
    },
    "scripts": {
        "browserify": "browserify src/index.js | uglifyjs -c 2> /dev/null > build/bundle.js",
        "build-fixture": "browserify --full-paths ./test/fixture/index.js > ./test/fixture/bundle.js && browserify ./test/fixture/index.js > ./test/fixture/bundle-no-full.js",
        "bundle-demo": "node lib/bundle-demo > index.html",
        "demo": "npm run prepublish && opener index.html",
        "prepublish": "mkdir -p build && npm run browserify && npm run rework && npm run bundle-demo",
        "rework": "node lib/bundle-css > build/style.css",
        "test": "node test | tap-spec"
    },
    "version": "1.3.2"
}
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
