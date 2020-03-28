+++
title = "Git submodule"
author = ["jirex"]
lastmod = 2020-03-28T22:05:20+08:00
tags = ["git"]
draft = false
+++

## 添加 {#添加}

```bash
git submodule add git@github.com:repo site-lisp/repo
```


## 删除 {#删除}

```bash
git -rm --cached site-lisp/repo
rm -rf site-lisp/repo
rm -rf .git/modules/repo

#remove submodule info
vim .git/config
vim .gitmodules
```
