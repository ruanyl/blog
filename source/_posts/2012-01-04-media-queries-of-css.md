---
layout: post
title:  "Media queries in css"
date:   2012-01-04 19:44:31
categories: CSS
tags: Css
author: Bigruan
---

An easy way to make your website "responsive"

```css
@media screen and (min-width:600px) {
  nav {
    float: left;
    width: 25%;
  }
  section {
    margin-left: 25%;
  }
}
@media screen and (max-width:599px) {
  nav li {
    display: inline;
  }
}
```

If screen width >= 600px, *nav,section* elements will display as this, and if screen width <= 599px, *nav,section* elements will display like that, quite easy!
