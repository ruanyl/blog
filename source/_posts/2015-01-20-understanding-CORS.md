---
layout: post
title:  "Understanding CORS"
date:   2015-01-20 21:51:22
categories: Server
tags: HTTP
author: Bigruan
---

#### What is CORS?

CORS stands for Cross Origin Resouce Sharing. It means that requests for resources from another domain than the domain where the requests are making.

For security reasons, some HTTP requests are restricted by [same origin policy](https://developer.mozilla.org/en/Same_origin_policy_for_JavaScript). For example an Ajax request, we can not make ajax request from domainA.com to request resource from domainB.com. But this could be painful if you are making a restful API which you host your API in another domain like: api.mydeomain.com.

#### When it is used?

As described in MDN:

```
Invocations of the XMLHttpRequest API in a cross-site manner, as discussed above.
Web Fonts (for cross-domain font usage in @font-face within CSS)
WebGL textures.
Images drawn to a canvas using drawImage.
```

#### How it work?

Here we talk about two kinds of cross-site request. They are *simple requests* and *preflight request*.

Simple request behaviour:

```
Client: Hey man, can I take/put some apples from/to your storage?
Server: No. --end
```

Preflight request behabiour:

```
Client: Hey man, can I take/put something from/to your storage?
Server: Yes please. (or No --end)
Client: Cool! Please give me some apples.
```

A simple cross-site request is one that(MDN):

```
Only uses GET, HEAD or POST. If POST is used to send data to the server, the Content-Type of the data sent to the server with the HTTP POST request is one of application/x-www-form-urlencoded, multipart/form-data, or text/plain.
Does not set custom headers with the HTTP Request (such as X-Modified, etc.)
```

Otherwise, it is a Preflight request. But, how a simple request actually looks like?

Take a simple GET request for example, if you open chrome dev tool and you will find something like this from http *request* headers:

```
GET /account/user/ HTTP/1.1
...
...
Origin: http://client.localhost
```

It tells the server: I am from http://client.localhost and I want to get user infomation(/account/user/).

Then server *response*:

```
HTTP/1.1 200 OK
...
...
Access-Control-Allow-Origin: *
Content-Type: application/json

[json data]
```

It tells the client: we allow anyone(as you can see:Access-Control-Allow-Origin: *) came to take user data from here and here is the data. If there is no Access-Control-Allow-Origin provided in response header, the browser will give you an error.

Preflight request is a little different. Client actually will have two requests. The first request is send with 'OPTIONS' method. If success, then make the actuall request. Take a POST request for an example:

First it makes a OPTIONS request:

```
OPTIONS /save/user/ HTTP/1.1
...
...
Origin: http://client.localhost
Access-Control-Request-Method: POST
```

It 'test' the server to see if it allows the origin domain and request method for the specific route.

Then the server response:

```
HTTP/1.1 200 OK
...
...
Access-Control-Allow-Origin: http://client.localhost
Access-Control-Allow-Methods: POST, GET, OPTIONS
Access-Control-Max-Age:3600
```
Server says OK, you are allowed and can use POST,GET,OPTIONS methods

Finally make the actuall POST request:

```
POST /save/user/ HTTP/1.1
...
...
Content-Type:application/json;charset=UTF-8
Origin:http://client.localhost
```


