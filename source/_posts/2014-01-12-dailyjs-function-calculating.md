---
layout: post
title:  "JS Excercise:Function Calculating"
date:   2014-01-12 20:09:45
categories: JS
tags: Javascript
author: Bigruan
---

Implementing functions like:

```javascript
five(minus(two())); //should return 3
seven(plus(one())); //should return 8
eight(times(three())); //should return 24
four(divideBy(two())); //should return 2
```

### solutions 1:
```javascript
var fun = function(num) {
  return function(operator) {
    return operator ? operator(num) : num;
  }
};
var zero = fun(0);
var one = fun(1);
var two = fun(2);
var three = fun(3);
var four = fun(4);
var five = fun(5);
var six = fun(6);
var seven = fun(7);
var eight = fun(8);
var nine = fun(9);

function plus(b) { return function(a) { return a + b; }; }
function minus(b) { return function(a) { return a - b; }; }
function times(b) { return function(a) { return a * b; }; }
function dividedBy(b) { return function(a) { return a / b; }; }
```
