---
title:  "Array in Javascript"
date:   2011-05-15 18:37:28
categories: JS
tags: Javascript
author: Bigruan
---

1.Create an Array.

```javascript
/** Create an array **/
var arrayObj = new Array();
arrayObj[0] = "obj1";
arrayObj[1] = "obj2";
arrayObj[2] = "obj3";

/** Create an array and specify(initial length) length,
 *  but the actual length can be more than 3
**/
var arrayObj = new Array(3);
arrayObj[0] = "obj1";
arrayObj[1] = "obj2";
arrayObj[2] = "obj3";

/** Create an array and assign values **/
var arrayObj = new Array("ojb1", "obj2", "obj3");

/** Simply you can do as this **/
var arrayObj = ["obj1", "obj2", "obj3"];

```

2.Access values

```javascript
var arrValue = arrayObj[1]; // get the value
arrayObj[1] = "newValue"; //assign a new value
```

3.Add items to an Array

```javascript
//Add one or more items to the end of the array, return the array length
arrayObj.push("newObj1", "newObj2");

//Add one or more items to the beginning of the array, return the array length
arrayObj.unshift("newObj1", "newObj2");

//At position 2, remove 2 items, and add "newObj1", "newObj2" to the end of the array
arrayObj.splice(2, 2, "newObj1", "newObj2");
```

4.Delete items from an Array

```javascript
//remove the last item of an array and return this item
arrayObj.pop();

//remove the first item of an array and return this item
arrayObj.shift();

//delete numbers of items from the specified position
arrayObj.splice(deletePos, deleteCounts);
```

5.Select items from an array or join two or more arrays

```javascript
//select items from position start to end as a new array and return it.
//end can be empty
arrayObj.slice(start, end);

//join several arrays
arrayObj.concat(array1, array2, array3);
```

6.Copy an array

```javascript
arrayObj.slice(0); //return a new copy of the array
arrayObj.concat(); //return a new copy of the array
```

7.Sort an array

```javascript
arrayObj.reverse(); //return the reverse of an array
arrayObj.sort();
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort(); //result:Apple,Banana,Mango,Orange

var points = [40,100,1,5,25,10];
points.sort(function(a,b){return a-b}); //result: 1,5,10,25,40,100
```

8.Array to string

```javascript
arrayObj.join(separator); //joint the items of an array with separator
```
