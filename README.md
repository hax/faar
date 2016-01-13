# FAst ARchiver for Node.js

## Why faar?

Because current packages for archive/unarchive (archiver, Decompress, tar-stream/tar-fs, etc.)
are too slow. (See [performance comparison](#Performance Comparison))

They are slow not because the code quality, but due to Node.js limitations on
usage of multi-core and file system.

The easiest way to fix that is just use full-fledged shell tools such as
`tar`, `pigz`, `lz4`... That's what this package do.


## Install
```sh
npm install faar
```

## Usage
```js
var fa = require('faar')

Promise.resolve(['./test1', './test2'])
	.then(items => {
		console.log('archiving', items)
		return fa.archive(items, './archives/test')
	})
	.then(arcFile => {
		console.log('...to', arcFile)
		return arcFile
	})
	.then(arcFile => {
		console.log('unarchiving', arcFile)
		return fa.unarchive(arcFile, './')
	})
	.then(items => {
		console.log('...to', items)
		return items
	})
```

## Configuration
```js
var fa = require('faar')

// register new archive format
fa.register('lzo', {
	compress: 'lzop',
	uncompress: 'unlzop',
})
fa.register('7z')
// prefer lzo, if not available fallback to gzip
fa.prefer(['lzo', 'pigz', 'gzip'])
```

## Built-in Configurations
### Archive Tools
gzip, pigz, zip, 7z, bzip2, xz, lzop, lz4
### Default Preference
lz4, pigz, gzip, zip

## Performance Comparison
TBD
