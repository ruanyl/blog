---
layout: post
title:  "Relearn javascript : New Sight of Function"
date:   2014-03-06 23:08:11
categories: JS
tags: Javascript
author: Bigruan
---

This post will not cover every part of javascript. what it going to include are something kind of 'new' to myself.

### 1.The method invocation pattern and function invocation pattern
When a function is invoked as a property of an object, we say it is invoked as a method.
when a method is invoked, *this* refers to the current object.

for example:
```javascript
var user = {
    "username" : "bigruan",
    "password" : "123456",
    "sayHello" : function() {
       return "Hello " + this.username;
    }
}
console.log(user.sayHello()); //Hello bigruan
```

When a function is not the property of an object, it is invoked as a function.

for example:
```javascript
var sayhello = function() {
    console.log("hello");
}
sayhello();
```

*However*, when function was invoked like this, *this* will be bind to global object.

for example:
```javascript
var user = {
    "username" : "bigruan",
    "password" : "123456",
    "sayHello" : function() {
        function say() {
            return "Hello " + this.username;
        }
        return say();
    }
}
console.log(user.sayHello()); //Hello undefined
```

the output could be undefined! how can we do with this situation?

the solution could be very easy:
```javascript
var user = {
    "username" : "bigruan",
    "password" : "123456",
    "sayHello" : function() {
        var that = this; //one line hacker
        function say() {
            return "Hello " + that.username;
        }
        return say();
    }
}
console.log(user.sayHello()); //Hello undefined
```

>other invocation pattern like apply and new will not discussed.

### 2.Arguments

When a function is invoked, an array named *arguments* can be accessed in the function which contains all the parameters.
Even the ones that are not showed in the function parameters.

```javascript
function sum() {
    var i,
        sum = 0;
    for(i=0; i<arguments.length; i++) {
        sum += arguments[i];
    }
    return sum;
}

console.log(sum(1, 2, 3, 4, 5));
```
