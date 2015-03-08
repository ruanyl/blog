---
layout: post
title:  "Javascript Regular Expression in Detail"
date:   2015-03-07 09:21:30
categories: Javascript
tags: RegExp
author: Bigruan
---

Regular Expression is widely used in the programmig world but it may not been used so frequently in someone's daily work. Like me, sometime i forgot
the syntax of Regular Expression or just not able to recall the relevant Javascript functions. Then i will need to search the Regular Expression manual and
read Javascript references. This post will cover some of the commonly used functions of Regular Expression in Javascript.

### Creating a Regular Expression

There are two ways to create a Regular Expression in Javascript: a *literal notation* and a *RegExp constructor*, for example:

```javascript
var regex = /^ab+c$/ig; // literal notation: /pattern/flags
var regex = new RegExp('^ab+c$', 'ig'); // RegExp constructor: new RegExp(pattern[, flags])
```

#### Pattern string

When use literal notation, pattern is surrounded with two slash */pattern/* while in RegExp constructor it's a normal string, but notice that when using 
constructor way the pattern string should be escaped. for example:

```javascript
var regex = /\d+/;
var regex = new RegExp('\\d+'); // double back slash are used
```

#### Flags

A flag can be any of the combination of the following values:

```javascript
i //ignore cases
g //global match
m //multiline; treat beginning and end characters (^ and $) as working over multiple lines
```

See details at [MND](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp)


### Methods you should know
#### 1.RegExp.prototype.test()
If you simply want to find whether a pattern is found in a string, test() method would be a good choice. It returns true or false.

For example: test if a string has a pattern
```javascript
var regex = /^ab+c/;
regex.test('abcdef'); //true
```

What if you want to find out how many times a pattern appears in a tring?
Another important property you should know about RegExp object: *RegExp.lastIndex*.
```javascript
// find out how many times a number group appears in a string
var regex = /\d+/g; // with g flag!
var str = 'aa23bb22cc1dd';
var num = 0;
while (regex.test(str) !== false) {
  var msg = 'Next match starts at ' + regex.lastIndex;
  num++;
  console.log(msg);
}
console.log('There are ' + num + ' groups of number in this string'); // num = 3
```
You can find that value of *lastIndex* updated when everytime run test() method. 
*But! NOTICE!! lastIndex updated ONLY IF you have 'g' flag in your Regular Expression.*


#### 2.RegExp.prototype.exec()
The exec() method take a string and execute the a search on this string. It return an Array or null.

If you understand the return Array, then you understand most of Javascript RegExp :)

Let see an example in detail. 
Say you want to find out the country code, area code and phone number of a full phone number string. for example: +86-028-84553673
let's do an stupid simple test ;)

```javascript
var regex = /\+(\d{2})-(\d{3})-(\d{8})/g;
var phoneNum = 'Tom: +86-028-84553673, Juha: +86-010-23457788';
var result;
while ((result = regex.exec(phoneNum)) !== null) {
  var msg = 'Found ' + result[0];
  msg += '\nCountry Code: ' + result[1];
  msg += '\nArea code: ' + result[2];
  msg += '\nNumber: ' + result[3];
  console.log(msg);
}
```
Output:
```bash
Found +86-028-84553673
Country Code: 86
Area code: 028
Number: 84553673
Found +86-010-23457788
Country Code: 86
Area code: 010
Number: 23457788
```

Let's take a look at the *result* object:

```bash
result[0]       : the full string that matched the pattern
result[1]...[n] : the pattern that you are willing to preserve which you placed in Parentheses ()
```

That't it!
