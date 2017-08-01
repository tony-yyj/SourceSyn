---
title: git 强制覆盖远程分支
tags: git
categories: git
abbrlink: 1824055434
abbrlinkurl: 'http://www.mashangxue123.com/1824055434'
date: 2017-07-29 23:16:15
---
如果远程主机的版本比本地版本更新，推送时Git会报错，要求先在本地做 `git pull` 合并差异，然后再推送到远程主机。
这时，如果你一定要推送，可以使用 `--force` 选项。
```
git push --force origin 
```
上面命令使用 `--force` 选项，结果导致远程主机上更新的版本被覆盖。
除非你很确定要这样做，否则应该尽量避免使用 `--force` 选项。

<!-- more -->
