---
title: git 强制覆盖本地
date: 2017-07-29 23:12:25
tags: git
categories: git
---
命令：
```bash
git fetch --all  
git reset --hard origin/master 
```

说明:
- `Git fetch`命令下载最新的更新远程，但**不合并**或本地文件变基址。
- `Git reset` master分支重置你刚才取下的。该`-hard`选项更改的所有文件到你的工作树origin/master。

重要提示:
- 当地所有的更改将丢失。
- 尚未被推送的任何本地提交将丢失。

要下载一些其他分支的更改使用以下命令:
```
$ git reset --hard origin/other_branch
```
<!-- more -->
