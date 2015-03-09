---
title:  "Long press in javascript"
date:   2013-01-28 21:06:48
categories: JS
tags: Javascript
author: Bigruan
---

Way to detect a long press event.

```javascript
var pressTimer

$("a").mouseup(function(){
  clearTimeout(pressTimer)
  // Clear timeout
  return false;
}).mousedown(function(){
  // Set timeout
  pressTimer = window.setTimeout(function() { ... your code ...},1000)
  return false;
});
```

This can also be used in touch event.
