---
layout: post
title:  "Relearn javascript : Basic Object Concepts"
date:   2014-02-23 18:18:29
categories: JS
tags: Javascript
author: Bigruan
---

### 1.Define an Object

```javascript
//define an empty object
var user = {}

//or with initial properties
var user = {
    "userName" : "bigruan",
    "passwd"   : "123456"
}
```

It is not necessary to surround properties with quote if property name is a legal javascript name.
For example: quotes are necessary for user-name but optinal for userName.

>Legal javascript name: contains letters(upper case or lower case), digitals, _ and $ , but should not begin with digital

Object can nest:

```javascript
var user = {
    userName : "bigruan",
    passwd   : "123456",
    car : {
        brand : "Audi",
        price : 1000
    }
}
console.log(user.car.price); //1000
```

### 2.Object Property values

```javascript
//access by [] or .
console.log(user["userName"]); //bigruan
console.log(user["car"]["price"]); //1000
console.log(user.userName); //bigruan
console.log(user.car.price); //1000

//if property not defined, the value will be undefined
console.log(user.child); // undefined
console.log(user["child"]); // undefined

//if trying to retrieve value from undefined, there will be a TypeError.
var childName = user.child.name; //TypeError
//A good practice to avoid this error
var childName = user.child && user.child.name;
```


Update property value. if property name was defined, value will be replaced by the new value. if there is no such property, a new property will be added to this Object.
```javascript
user.userName = "yulong"; //value of userName is updated
user.child = {}; //new property child is added
```

Retrieve value by for in loop.

```javascript
for(var key in user) {
    console.log(user[key]);
}
```

### 3.Object passed by reference and can not be copied

```javascript
var user2 = user;
user2.userName = "bigruan2";
console.log(user.userName);
// userName of user is bigruan2,
// because user and user2 are references to the same object
```
