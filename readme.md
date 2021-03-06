# gulp-chflags [![Build Status](https://travis-ci.org/affirmix/gulp-chflags.svg?branch=master)](https://travis-ci.org/affirmix/gulp-chflags)

> Change permissions of [Vinyl](https://github.com/wearefractal/vinyl) files

## Install

```
$ npm install --save-dev gulp-chflags
```

## Usage

```js
var gulp = require('gulp');
var chmod = require('gulp-chflags');

gulp.task('default', function () {
	return gulp.src('src/app.js')
		.pipe(chflags(23))
		.pipe(gulp.dest('dist'));
});
```

or

```js
var gulp = require('gulp');
var chmod = require('gulp-chflags');

gulp.task('default', function () {
	return gulp.src('src/app.js')
		.pipe(chflags([
			'uchg',
			'uunlnk'
		]))
		.pipe(gulp.dest('dist'));
});
```

## API

### chflags(flags)

#### flags

Type: `number`, `array`

Can either be a [chflags](http://ss64.com/osx/chflags.html) octal number or an array with the individual flags specified.

Values depends on the current file, but these are the possible keys:

```js
{
	'hidden',
	'opaque',
	'nodump',
	'uappnd',
	'uappend',
	'uchg',
	'uchange',
	'uimmutable',
	'uunlnk',
	'uunlink',
	'arch',
	'archived',
	'sappnd',
	'sappend',
	'schg',
	'schange',
	'simmutable',
	'sunlnk',
	'sunlink'
}
```

Putting the letters no before an option causes the flag to be turned off. For example:

* `'uchg'`: Means the file cannot be changed
* `'nouchg'`: Means the file can be changed (immutable bit cleared)
* `'hidden'`: Will set the hidden flag
* `'nohidden'`: Will remove the hidden flag

## Tip

Combine it with [gulp-filter](https://github.com/sindresorhus/gulp-filter) to only change permissions on a subset of the files.

```js
var gulp = require('gulp');
var gFilter = require('gulp-filter');
var chmod = require('gulp-chmod');

var filter = gFilter('src/cli.js');

gulp.task('default', function () {
	return gulp.src('src/*.js')
		// filter a subset of the files
		.pipe(filter)
		// make them immutable
		.pipe(chflags(['uchg']))
		// bring back the previously filtered out files
		.pipe(filter.restore())
		.pipe(gulp.dest('dist'));
});
```

## Attribution

Credit goes to [Sindre Sorhus](https://github.com/sindresorhus) for providing an excellent template for this project by means of [gulp-chmod](https://github.com/sindresorhus/gulp-chmod) and [gulp-chown](https://github.com/sindresorhus/gulp-chown).
