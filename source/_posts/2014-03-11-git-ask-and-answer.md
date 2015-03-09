---
title:  "Git ask and answer"
date:   2014-03-11 15:08:45
categories: Git
tags: Git
author: Bigruan
---

### 1.How to use git to checkout remote branch?

First you need to fetch those new remote branches by using:

```bash
git fetch origin
```

```bash
show and see all the branches:
```

```bash
git branch -v -a
```

Then checkout the branch you are interested in:

for example: a remote branch named *test* and you want to checkout this branch by using the name *mybranch*

```bash
git checkout -b mybranch origin/test
```

If your Git version >= 1.6.6 you can simply by running:

```bash
git checkout test
```
