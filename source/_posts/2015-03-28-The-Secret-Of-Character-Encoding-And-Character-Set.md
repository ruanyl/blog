---
title:  "The Secret of Character Encoding and Character Set"
date:   2015-03-28 23:29:14
categories: Others
tags: Encoding
author: Bigruan
---

It is a common issue that your page get messed up with non-English characters, for example Chinese and some European characters are displayed as '??? ???? ?????' or '���� ����'.
Sometimes it's even worse if you need to communicate with another system that has different character encoding from yours. for example: GBK(GB18030) and UTF-8

### What is Character Encoding and Character Set?
Some concepts we need to make clear before we continue. People usually dont have a clear distinction between Character Encoding and Character Sets.
Someone may even ask what's the difference between UTF-8 and Unicode.

*Unicode* is a Character Set, just as the name says, it's a set of characters which mapped to a set of unique numbers(code point). for example in the Unicode world,
A is 41, an 1 is 31 and 💩 is 1F4A9

```
A --- U+0041
1 --- U+0031
💩 --- U+1F4A9
```

While Character Encoding is a set of mappings between the numbers of Character Sets and the bytes in computer. for example in UTF-8:

```
U+0041  --- 01000001
U+0031  --- 00110001
U+1F4A9 --- 11110000 10011111 10010010 10101001
```

The characters are translated to binary and can be stored in disk or memory now. It's not that hard, right?

### What are those Mysterious ??? and � ?
We know that data are transfered as binary in the wire, so when a browser get the binary data, it have to know what Character Encoding the data was used
so that it can represent the right Character as expected.

So, in a browser you must tell the Character Encoding otherwise the browser will guess or it will use the default Character Encoding and that's horrible...

### Tell a browser what Character Encoding you are using

1.Specify Encoding in the http response header

```
Content-Type:text/html; charset=UTF-8
```

In php you can do this by setting the following in php.ini
```
default_charset = "UTF-8"
```

or if you are using Apache server, in httpd.conf and add:
```
AddDefaultCharset utf-8
```

But this is not a good way, think about that if you have a webserver that serves couple of websites with different Encoding(bad idea..)
So a better way could:

2.Use HTML *meta* tag
```html
<!--HTML 4, which default is ISO-8859-1-->
<meta http-equiv="Content-Type" content="text/html; charset=utf-8">

<!--HTML 5, default is UTF-8-->
<meta charset="utf-8">
```

### Make sure that your data are well encoded
You have told the browser what Encoding you are using. What if you are using mixed Encoding in your server side? That could be happened.

for example you have page a.php which file encoding is utf-8 but it read some content from a file which is another file encoding,
for example GB18030(GBK)
```
<?php
$req = file_get_contents('test.txt'); // test.txt is in GB18030(GBK)
?>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf8"/>
        <title>index</title>
    </head>
    <body>
        <form id="tForm" action="/form.php" method="GET" accept-charset="utf-8" enctype="multipart/form-data">
        输入：<input type="text" name="req" value="<?=$req?>"/>
        </form>
    </body>
</html>
```
you will see part of the page is correct but the input value maybe incorrect. Now when you submit the form, the server will never get the right value.
And think about reading a database with different encoding? That's terrible right?

There are thousands of articles that suggest to use UTF-8 and Unicode, so please do that to make yours and others life easy.
