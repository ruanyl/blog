---
layout: post
title:  "Understand methods position() and offset() in jquery"
date:   2011-09-12 19:28:36
categories: JS
tags: Javascript Nodejs
author: Bigruan
---

To get the position of the elements sometime can be awful. Understanding jquery position() and offset() probably do great help.
It is important to make the difference of the two function clearly.

Usage:
```javascript
    $('.div').offset().top;
    $('.div').offset().left;
    $('.div').position().top;
    $('.div').position().left;
```

Offset: get the element's postion relative to the current window. [Demo](http://82.130.25.39:4000/demo/jquery-offset-positon.html)

position: get the element's postion relative to its positioned(relative or absolute) parent element. [Demo](/demo/jquery-offset-positon.html)

![image](/images/jquery-position-offset.jpg)
