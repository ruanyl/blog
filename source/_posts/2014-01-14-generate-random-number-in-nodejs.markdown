---
title:  "Generate random string in nodejs"
date:   2014-01-14 18:02:51
categories: JS
tags: Javascript Nodejs
author: Bigruan
---

>ref:http://nodejs.org/api/crypto.html

```javascript
var crypto = require('crypto')
var sid = function() {
    var current_date = (new Date()).valueOf().toString();
    var random = Math.random().toString();
    var num = crypto.createHash('sha1').update(current_date + random).digest('hex');
    return num;
}

for(var i=0; i<3; i++) {
console.log(sid());
}
```
