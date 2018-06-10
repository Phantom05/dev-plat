# Developement Platform
I have made the **build system** that NPM uses as a platform.


## Developement Structure List
+ ### [Gulp Platform][0]
[0]:https://github.com/Phantom05/dev-plat/tree/master/gulp

## Motivation
Every time I use it, it takes too long and I made it easy to download and use it immediately.

## Build status
Because you need to use NPM, you need Node js and you need to install npm.

[![Build Status](https://travis-ci.org/akashnimare/foco.svg?branch=master)](https://nodejs.org/)

## Code style
I followed the standard as follows.

[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat)](https://github.com/Phantom05/dev-plat/blob/master/gulp/gulpfile.js)
 
## Screenshots
We will update if there are many requests.

## Tech/framework used
Ex. -

<b>Built with</b>
- [Node.js](https://nodejs.org/)

## Features
What makes your project stand out?

## API Reference

Depending on the size of the project, if it is small and simple enough the reference docs can be added to the README. For medium size to larger projects it is important to at least provide a link to where the API reference docs live.

## Tests
Describe and show how to run the tests with code examples.

## How to use?
If people like your project they’ll want to learn how they can use it. To do so include step by step guide to use your project.

```js
const gulp = require('gulp');
const webserver = require('gulp-webserver');
const uglify = require('gulp-uglify');
const minifyHtml = require('gulp-minify-html');
const sass = require('gulp-sass');
const livereload = require('gulp-livereload');
const babel = require('gulp-babel');
const uglifyCss = require('gulp-uglifycss');
const concat = require('gulp-concat');
const imageMin = require('gulp-imagemin');
const watch = require('gulp-watch');
const rename = require('gulp-rename');
const pump = require('pump');

const src = 'public/src';
const dist = 'public/dist';

const paths = {
  js: src + '/js/*.js',
  scss: src + '/sass/*.scss',
  html: src + '/**/*.html',
  cssmin: dist + '/css/*.css'
}

//js
gulp.task('babel', function () {
  gulp.src(paths.js)
    .pipe(babel({
      presets: ['env']
    }))
    .pipe(gulp.dest(dist + '/js'))
});

gulp.task('combine-js', function () {
  return gulp.src([dist + '/js/*.js', '!' + dist + '/js/script.js'])
    .pipe(concat('script.js'))
    .pipe(gulp.dest(dist + '/js'));
});

gulp.task('compress-js', function (cb) {
  pump([
      gulp.src(dist + '/js/script.js'),
      uglify({
        mangle: true,
      }),
      rename('script.min.js'),
      gulp.dest(dist + '/min')
    ],
    cb
  )
});

// css
gulp.task('sass', function () {
  gulp.src(paths.scss)
    .pipe(sass())
    .pipe(gulp.dest(dist + '/css'))
});

gulp.task('uglifyCss', function () {
  gulp.src(dist + '/css/*.css')
    .pipe(uglifyCss())
    .pipe(rename(function(path){
      // path.dirname+='/cica'; //폴더만들고 그안에 넣음
      path.basename+='.min';
      // path.extname ='.md' // 확장자바꿈
    }))
    .pipe(gulp.dest(dist + '/min'))
});

//html
gulp.task('minifyHtml', function () {
  gulp.src(paths.html)
    .pipe(minifyHtml())
    .pipe(gulp.dest(dist + '/'))
});

gulp.task('watch', function () {
  gulp.watch(paths.js, ['js:combine']);
  gulp.watch(paths.scss, ['scss:compile']);
});


gulp.task('default', ['babel', 'combine-js', 'compress-js', 'sass', 'uglifyCss', 'minifyHtml']);
```

## Contribute

[Phantom05](https://github.com/Phantom05)

#### Anything else that seems useful

## License
A short snippet describing the license (MIT, Apache etc)

MIT © [Phantom05](https://github.com/Phantom05)

