# @zkochan/cmd-shim

The cmd-shim used in npm to create executable scripts on Windows,
since symlinks are not suitable for this purpose there.

On Unix systems, you should use a symbolic link instead.

[![Build Status](https://img.shields.io/travis/ForbesLindesay/cmd-shim/master.svg)](https://travis-ci.org/ForbesLindesay/cmd-shim)
[![Dependency Status](https://img.shields.io/david/ForbesLindesay/cmd-shim.svg)](https://david-dm.org/ForbesLindesay/cmd-shim)
[![NPM version](https://img.shields.io/npm/v/cmd-shim.svg)](https://www.npmjs.com/package/cmd-shim)

## Installation

```
npm install @zkochan/cmd-shim
```

## API

### cmdShim(from, to, opts?, cb)

Create a cmd shim at `to` for the command line program at `from`.
e.g.

```javascript
var cmdShim = require('@zkochan/cmd-shim');
cmdShim(__dirname + '/cli.js', '/usr/bin/command-name', function (err) {
  if (err) throw err;
});
```

### cmdShim.ifExists(from, to, opts?, cb)

The same as above, but will just continue if the file does not exist.
Source:

```javascript
function cmdShimIfExists (from, to, cb) {
  fs.stat(from, function (er) {
    if (er) return cb()
    cmdShim(from, to, cb)
  })
}
```

### opts

* `opts.preserveSymlinks` - *Boolean* - if true, `--preserve-symlinks` is added to the options passed to NodeJS.

```javascript
var cmdShim = require('@zkochan/cmd-shim');
cmdShim(__dirname + '/cli.js', '/usr/bin/command-name', { preserveSymlinks: true }, function (err) {
  if (err) throw err;
});
```
