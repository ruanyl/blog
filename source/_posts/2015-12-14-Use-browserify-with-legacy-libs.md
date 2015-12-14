---
title:  "Use browserify with legacy libs"
date:   2015-12-14 22:45:19
categories: JS
tags: browserify
author: Bigruan
---

### The problem:

Browserify makes your frontend javascript more modularized and it helps to organize the frontend codes
much better. But only use browserify is not enough if you are using some legacy libs. Which means such
libs are not qualified for npm publication. for example some libs just simply use a global variable: `window.Module`

### Introduce to browserify-shim:

For those libs which expose themselves as `window.Module`, add the following to your `package.json`:

```
  "browserify": {
    "transform": [
      "browserify-shim"
    ]
  },
  "browserify-shim": {
    "module": "global:Module",
  }
```
What browserify-shim does here is it replaces:
```
var module = require('module')
```
with:
```
var module = (typeof window !== "undefined" ? window.Module : typeof global !== "undefined" ? global.Module : null)
```
[Why not just use var module = window.module](https://github.com/thlorenz/browserify-shim#why-not-just-var-three--windowthree)
