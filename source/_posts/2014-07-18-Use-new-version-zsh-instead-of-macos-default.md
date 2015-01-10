---
layout: post
title:  "Use new version of zsh instead of Mac os default"
date:   2014-07-18 00:16:39
categories: Server
tags: Zsh
author: Bigruan
---
Install zsh from [Homebrew](http://brew.sh/):

```bash
$ brew install zsh
```

Add zsh to default shell lists:

```bash
$ sudo vim /etc/shells
/bin/bash
/bin/csh
/bin/sh
/bin/tcsh
/bin/zsh
/usr/local/bin/zsh #new zsh that installed by homebrew
```

Change the shell for the current user:

```bash
$ chsh -s /usr/local/bin/zsh
```
