---
layout: post
title:  "Ways to clear float in css"
date:   2011-05-12 12:32:39
categories: CSS
tags: Css,Html
author: Bigruan
---

There are ways to clear float in css, but I choose the following methods.

```css
/*********** simple method **************/
.clearfix:before, .clearfix:after {
    content:"";
    display:table;
}
.clearfix:after{
    clear:both;
    overflow:hidden;
}
.clearfix{
    zoom:1;
}
/************ classic method ************/
.clearfix:after {
    visibility: hidden;
    display: block;
    font-size: 0;
    content: " ";
    clear: both;
    height: 0;
}
* html .clearfix             { zoom: 1; } /* IE6 */
*:first-child+html .clearfix { zoom: 1; } /* IE7 */
```

Tip: Add the class 'clearfix' to the parent element of the float elements.
