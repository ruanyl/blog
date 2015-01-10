---
layout: post
title:  "The Difference Between Apply and Call in Javascript"
date:   2011-11-14 19:31:28
categories: JS
tags: Javascript
author: Bigruan
---

*Apply* and *Call* are almost the same in javascript, the difference is the way they handle function arguments.

They are almost the same:

```javascript
var person1 = {
  name : 'foo',
  age  : 20
};

var person2 = {
  name : 'bar',
  age  : 21
};

var sayHello = function() {
  console.log('Hello ' + this.name);
};

sayHello.call(person1); //output: "Hello foo"
sayHello.call(person2); //output: "Hello bar"
```

However, *Call* accept the first argument as its context and the subsequent arguments are passed as the arguments of the function which invoke *Call*.

While *Apply* accept the first argument as its context but the second argument is an array, which then unpacked as arguments of the function.

```javascript
var sayHello = function(action, target) {
  console.log(this.name + ' ' + action + ' ' + target);
};

sayHello.call(person1, 'hate', 'me'); //foo hate me
sayHello.apply(person2, ['love', 'you']); //bar love you
```

There will be restriction when the number of arguments is not known in advance.

For example when we write a route function,

```javascript
var sayHello = function(action) {
  console.log(action + ' ' + this.name);
};

var update = function(name, age) {
  this.name = name;
  this.age  = age;
  console.log(this.name + ':' + this.age);
}

var router = function(person, method, args) {
  method.apply(person, args);
}

router(person1, sayHello, ['Hello']);
router(person2, update, ['bigruan', 25]);
```
