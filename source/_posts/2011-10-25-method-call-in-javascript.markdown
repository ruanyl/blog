---
layout: post
title:  "Method Function.prototype.call() in Javascript"
date:   2011-10-25 20:12:21
categories: JS
tags: Javascript
author: Bigruan
---

The method call() allows changing *this* object with a specified *thisObj*.

Usage:

>fun.call([thisObj[, arg1[, arg2[,  [, argN]]]]])

Example 1: Call a method which a object does not have

```javascript
function add() {
    console.log(this.a+this.b);
}

function iDontKnowAdd(a, b) {
    this.a = a;
    this.b = b;
}

var i = new iDontKnowAdd(3, 1);
add.call(i);

//Output: 4
```

This piece of code means that: execute function *add* in object *iDontKnowAdd*.

>"Note: in javascript Function is Object, Function name is the reference of Function Object."

Example 2: Achieve inherit by using call()

```javascript
function Class1() {
    this.showTxt = function(txt) {
        console.log(txt);
    }
}

function Class2() {
    Class1.call(this);
}

var c2 = new Class2();
c2.showTxt("abc");
//Output: abc
```

*Class1.call(this)* means executing function Class1 in the context of Class2.
while executing: *var c2 = new Class2()*, it can be regard as *Class1.call(c2)*.
And *this* in Class1 refers to *c2*, then *c2.showTxt = function(txt)...*.
definitely, c2 now has function showTxt().

But if we write the code like this:

```javascript
function Class1() {
    function showTxt(txt) {
        console.log(txt);
    }
}

function Class2() {
    Class1.call(this);
}

var c2 = new Class2();
c2.showTxt("abc");
//Output: Error
```

There will be error. We can see that, this is not 'real' Inherit.
