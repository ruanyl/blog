---
title:  "How to use git reset"
date:   2014-01-30 21:19:18
categories: Git
tags: Git
author: Bigruan
---

### Q1: How to undo git pull?
Actually git pull do two things, first run git fetch and then git merge.

If there are conflicts, merge will not be commit to local repo. So, just run the following command to reset your working directory and stating area.

```bash
git reset --hard
```

If there is not conflict, the merge will commit to the local repo, if you want to reset git pull immediatetly, run the following command to reset local repo, stating area and working directory to the previous commit.

```bash
git reset --hard HEAD^
```

### Q2: How to undo git add?

```bash
git reset
```

or:

```bash
git reset HEAD
```

They are the same.

What this command do is to use local repo to replace stating area. All files that add to stating area will be affected.

What if just some specified files? Then you can run:

```bash
git reset -- filenmae
```

### Q3: How to undo git commit if I am not satisfied with the comment?

```bash
git reset --soft HEAD^
```

By running reset with _--soft_ the working directory and stating area will not change but the local repo will be reset to specified ref. for example here is _HEAD^_ which means the previous one commit.

![image](/images/local-remote.png)
