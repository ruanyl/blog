---
title:  "JSON in Javascript"
date:   2012-02-01 19:19:48
categories: JS
tags: Javascript
author: Bigruan
---

### 1.Create JSON
You can create it like this:
```javascript
var foo = {
    "name" : "Ruan",
    "age"  : 25,
    "bar"  : {
        "name" : "Qiu",
        "age"  : 24
    }
}
```

or like this:
```javascript
var foo = {},
    bar = {};
foo.name = "Ruan";
foo.age = 25;

bar.name = "Qiu";
bar.age = 24;

foo.bar = bar;
```


### 2.Access value in a JSON object
```javascript
console.log(foo.name); //output: Ruan
console.log(foo.bar.name); //output: Qiu
```
or
```javascript
console.log(foo["name"]);
console.log(foo["bar"]["name"]);
```

### 3.Get values by loop
```javascript
for(var key in foo) {
    console.log(foo[key]);
}
```

Someone may say that it is exactly javascript object, so what is the difference between json and javascript object?

JSON is:

1. It is language agnostic data-interchange format.
2. The syntax of JSON was inspired by the JavaScript Object Literal notation, but there are differences between them.

>ref:http://stackoverflow.com/questions/3975859/what-are-the-differences-between-json-and-javascript-object

For example, in JSON all keys must be quoted, while in object literals this is not necessary:

```javascript
// JSON:
{ "foo": "bar" }

// Object literal:
var o = { foo: "bar" };
```

Javascript object can be convered to JSON format by JSON.stringify(obj) which keys/properties names will be quoted automatically.
However, it is mandatory(good behavior) to use double quotes when define a JSON object.

### 4.Use native JSON
```javascript
//Convert a JavaScript object into a JSON string
var jsonString = JSON.stringify(foo);
//output: {"name":"Ruan","age":25,"bar":{"name":"Qiu","age":24}}

//Convert a JSON string into a JavaScript object
var jsonObj = JSON.parse(jsonstring);
//result: a javascript object
```

>+ NOTE: in JavaScript 1.8.5
>+ Starting in JavaScript 1.8.5 (Firefox 4), JSON.parse() does not allow trailing commas

```javascript
// both will throw a SyntaxError as of JavaScript 1.8.5
var jsObject = JSON.parse("[1, 2, 3, 4, ]");
var jsObject = JSON.parse("{ \"foo\" : 1, }");
```

>+ ref: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Using_native_JSON?redirectlocale=en-US&redirectslug=Using_native_JSON
