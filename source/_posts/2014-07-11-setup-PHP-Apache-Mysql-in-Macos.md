---
title:  "Setup PHP, Apache and Mysql in Macos"
date:   2014-07-11 21:32:39
categories: Server
tags: Php Apache Mysql
author: Bigruan
---

After setting up LAMP environment hundreds of times in Linux(Debian, Ubuntu), this is the first time that I do this in Mac OS.

Setting up LAMP environment is quite easy in Debian, you can use *apt-get* to install automatically or you can compile from source. But in Mac OS,
we use *Homebrew* to make everything as simple as possible.

### 1.PHP
Mac OS has PHP installed defualtly but if you want to install a specified version, the follow steps might make sense.

+   1. you should have *homebrew* installed.
+   2. homebrew formulars that you should tap in advance.
```bash
$ brew tap homebrew/homebrew-php
$ brew tap homebrew/versions
$ brew tap homebrew/dupes
```
+   3. brew install php53 --with-mysql

### 2.Apache
Mac OS has apache http server installed by default.
You can find the config file here: /etc/apache2/httpd.conf
And the default document root as it says in httpd.conf is: /Library/WebServer/Documents

```bash
$ vim /etc/apache2/httpd.conf
```

uncomment #LoadModule php5_module ..., and load *libphp5.so* you just installed
It should be something like:

```bash
LoadModule php5_module /usr/local/Cellar/php53/5.3.28/libexec/apache2/libphp5.so
```

### 3.Mysql

```bash
$ brew install mysql
```

### 4.Install php modules

For example: mcrypt
Homebrew can do this easily for you, but one thing should be noticed is that when using homebrew to install php module you should tell homebrew a specified php *version*, for example:

```bash
$ brew install php53-mcrypt
```

That's the basic steps to setup AMP environment in Mac OS quickly! Enjoy it!
