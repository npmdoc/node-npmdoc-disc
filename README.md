# api documentation for  [disc (v1.3.2)](https://github.com/hughsk/disc)  [![npm package](https://img.shields.io/npm/v/npmdoc-disc.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-disc) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-disc.svg)](https://travis-ci.org/npmdoc/node-npmdoc-disc)
#### A tool for analyzing the module tree of a browserify bundle or node project

[![NPM](https://nodei.co/npm/disc.png?downloads=true)](https://www.npmjs.com/package/disc)

[![apidoc](https://npmdoc.github.io/node-npmdoc-disc/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-disc_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-disc/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-disc/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-disc/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Hugh Kennedy",
        "email": "hughskennedy@gmail.com",
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
            "name": "hughsk",
            "email": "hughskennedy@gmail.com"
        }
    ],
    "name": "disc",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
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



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module disc](#apidoc.module.disc)
1.  [function <span class="apidocSignatureSpan">disc.</span>bundle (bundles, opts, callback)](#apidoc.element.disc.bundle)
1.  [function <span class="apidocSignatureSpan">disc.</span>json (bundles, callback)](#apidoc.element.disc.json)



# <a name="apidoc.module.disc"></a>[module disc](#apidoc.module.disc)

#### <a name="apidoc.element.disc.bundle"></a>[function <span class="apidocSignatureSpan">disc.</span>bundle (bundles, opts, callback)](#apidoc.element.disc.bundle)
- description and source-code
```javascript
function bundle(bundles, opts, callback) {
  bundles = Array.isArray(bundles)
    ? bundles
    : bundles ? [bundles] : []

  if (typeof opts === 'function') {
    callback = opts
    opts = {}
  }

  opts = opts || {}
  callback = callback || noop

  var header = opts.header || opts.button || ''
  var footer = opts.footer || ''

  return json(bundles, function(err, data) {
    if (err) return callback(err)

    data.mode = opts.mode || 'size'
    data = '<script type="text/javascript">'
      + ';window.disc = ('
      + JSON.stringify(data)
      + ');</script>'

    var script = '<script type="text/javascript">'
      + bundled().replace(/\/script/gi, '\\/script')
      + '</script>'

    callback(null, template()({
        scripts: script
      , styles: styles()
      , markdown: footer
      , header: header
      , data: data
    }))
  })
}
```
- example usage
```shell
...
var input = __dirname + '/index.js'
var output = __dirname + '/disc.html'

var bundler = browserify(input, {
  fullPaths: true
})

bundler.bundle()
  .pipe(disc())
  .pipe(fs.createWriteStream(output))
  .once('close', function() {
    open(output)
  })
'''
...
```

#### <a name="apidoc.element.disc.json"></a>[function <span class="apidocSignatureSpan">disc.</span>json (bundles, callback)](#apidoc.element.disc.json)
- description and source-code
```javascript
function json(bundles, callback) {
  var modules = flatten(bundles
    .map(String)
    .map(unpack)
  ).map(function(module) {
    if (typeof module === 'undefined') return callback(new Error(
      'Unable to compile one of the supplied bundles!'
    ))

    if (typeof module.id !== 'number') return module

    return callback(new Error(
      'Please recompile this browserify bundle using the --full-paths flag ' +
      '(when using the command-line interface) or with the fullPaths option ' +
      'set to true (when using the JavaScript API).'
    ))
  })

  modules = modules.filter(function(module) {
    return module && !isEmpty(module)
  })

  if (!modules.length) return

  var browserifyModules = modules.filter(fromBrowserify(true))
  var otherModules = modules.filter(function(module) {
    if (path.basename(module.id) === '_empty.js') return false
    if (browserifyModules.indexOf(module) === -1) return true
  })

  var root = commondir(otherModules.map(pluck('id')))

  browserifyModules.forEach(function(module) {
    var regex = /^.+\/node_modules\/browserify\/(?:node_modules\/)(.+)$/g

    module.id = module.id.replace(regex, function(_, subpath) {
      return path.resolve(root, 'browserify-core/' + subpath)
    })

    return module
  })

  uniq(modules, function(a, b) {
    return a.id === b.id ? 0 : 1
  }, true)

  var ids  = modules.map(pluck('id'))
  var main = path.basename(root)

  var byid = modules.reduce(function(memo, mod) {
    memo[mod.id] = mod
    return memo
  }, {})

  fileTree(ids, function(id, next) {
    var row = byid[id]

    next(null, {
        size: row.source.length
      , deps: Object.keys(row.deps).length
      , path: id
    })
  }, function(err, tree) {
    if (err) return callback(err)

    tree = { name: main, children: tree }
    dirsizes(tree)
    versions(tree)
    callback(null, tree)
  })
}
```
- example usage
```shell
...
A callback-style interface for disc: takes an array of 'bundles' (note: the
file contents and not the file names), calling 'callback(err, html)' with
either an error or the resulting standalone HTML file as arguments.

This currently mirrors how disc is currently implemented, but the stream API is
a little more convenient to work with.

### 'disc.json(bundles, callback)' ###

Takes an array of bundle contents (as strings, or Buffers), and gathers the
required data - calling 'callback(err, json)' with either an error or the
results.

## Palettes ##
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
