---
title:  "How to use javascriot sourcemap?"
date:   2014-07-18 00:16:39
categories: JS
tags: Javascript
author: Bigruan
---

### 1.What is sourcemap?
A sourcemap is a file which contains the mapping between the minified(concated, uglified) file and the original files.

### 2.Why sourcemap?
If you want to keep your client side code readable and easy to debug after compressing, sourcemap will play tricks.

### 3.How to use sourcemap?

1.Enable sourcemap in chrome dev tools.

2.Generate sourcemap by using gulp(or grunt or whatever tools you like)

here is a sample configuration of Gulpjs.

```javascript
var gulp = require('gulp');

var concat = require('gulp-concat');
var uglify = require('gulp-uglify');
var sourcemaps = require('gulp-sourcemaps');

var paths = {
  scripts: 'src/**/*.js'
};

gulp.task('scripts', function() {
  // Minify and copy all JavaScript (except vendor scripts)
  // with sourcemaps all the way down
  return gulp.src(paths.scripts)
    .pipe(sourcemaps.init())
      .pipe(concat('all.js'))
      .pipe(uglify())
    .pipe(sourcemaps.write())
    .pipe(gulp.dest('build/js'));
});

// Rerun the task when a file changes
gulp.task('watch', function() {
  gulp.watch(paths.scripts, ['scripts']);
});

// The default task (called when you run `gulp` from cli)
gulp.task('default', ['watch', 'scripts']);

```
