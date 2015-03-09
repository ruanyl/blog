---
title:  "Null and Undefined in javascript"
date:   2012-02-15 21:39:04
categories: JS
tags: Javascript
author: Bigruan
---

### 1.Null and Undefined
In javascript an undefined variable is a variable that never been declared or never assigned a value.

```javascript
var foo;
console.log(foo); // The output will be: undefined
```

If you assign _foo = null_. Then foo will be null which is a javascript object

```javascript
var foo;
console.log(typeof foo); //output: undefined

foo = null;
console.log(typeof foo); //output: object
```

### 2.Confuse of working with "==" and "===".
_===_ means strictly equal which will check both _type_ and _value_.

Servral samples:

```javascript
null === null            # => true
undefined === undefined  # => true
undefined === null       # => false
undefined == null        # => true
```

### 3.What is false in javascript?

```javascript
if(!false) {
    //definitely, false is false
}
if(!undefined) {
    //undefined is false
}
if(!null) {
    //null is false
}
if(!'') {
    //empty string '' is false
}
if(!0) {
    //numver 0 is false
}
if(!NaN) {
    //numver NaN is false
}
```

Except these value, others could be regard as true.

>ref: http://stackoverflow.com/questions/5101948/javascript-checking-for-null-vs-undefined-and-difference-between-and
