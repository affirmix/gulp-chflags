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
		.pipe(chflags({
			uchg: true,
			uunlnk: true
		}))
		.pipe(gulp.dest('dist'));
});
```

## API

### chflags(mode)

#### mode

Type: `number`, `object`

Can either be a [chflags](http://ss64.com/osx/chflags.html) octal number or an object with the individual flags specified.

Values depends on the current file, but these are the possible keys:

```js
{
	hidden: true,
	opaque: true,
	nodump: true,
	uappnd: true,
	uappend: true,
	uchg: true,
	uchange: true,
	uimmutable: true,
	uunlnk: true,
	uunlink: true,
	arch: true,
	archived: true,
	sappnd: true,
	sappend: true,
	schg: true,
	schange: true,
	simmutable: true,
	sunlnk: true,
	sunlink: true
}
```

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
		.pipe(chflags({ uchg: true }))
		// bring back the previously filtered out files
		.pipe(filter.restore())
		.pipe(gulp.dest('dist'));
});
```
