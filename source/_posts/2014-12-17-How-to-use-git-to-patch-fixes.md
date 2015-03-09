---
title:  "How to use git to patch fixes"
date:   2014-12-17 19:58:22
categories: Git
tags: Git
author: Bigruan
---

## How to use git to patch fixes?

If you need to apply patches from a new release of an open source software that used in your project. However, you lost all the git history of the original repo(for example download release.tar.gz directly) or you just want to apply some of those Fixed commits. Then *git format-patch* probably a good choice.

### Creating the patch

```bash
git format-patch --signoff --binary 55befce..1b30d93
```

This command means that creating patch from commit '55befce' to '1b30d93'. And --binary will output a binary diff that you can use to apply the changes to binary file. Actually, --binary is enabled by default. But the difference is that if you create patch files with --binary, all the patch files will use full index instead of the first handful of characters.

this is the difference when outputting patch files.

```bash
index 5150093..ebbca95 100644
index 51500932980c91ef1e6a656ce01dafbca089d148..ebbca9519e7c742eca5bb58f244e704605155474 100644
```

while if there is no --binary, for those not binary files will use the short one and binary files will use the longer one. So, i guess that's really doesn't matter whether use --binary or not.

But if you dont want to output the diff of binary files, use *--no-binary* instead.

### Applying the patch

Now you have a list of \*.patch files. Run the following command to apply it.

```bash
git am -3 path/to/*.patch
```

*-3* means that when git trys to apply this patch, it'll do a 3-way merge. If there is no conflict, a new commit will be auto commited. if there is conflict, resolve the conflicts then:

```bash
git am --continue
```

If error happened and git can not auto merge the files, you will need to apply the patch manully. Open the patch files and find what has changed, then just do it manully.. Abort the current process first:

```bash
git am --abort
```

when you've done it manully, then commit it as normal.
