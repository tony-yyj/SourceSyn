---
title: Linux 基本命令：复制 删除
tags:
  - Linux命令
categories: Linux
abbrlink: 2636495291
date: 2017-09-06 20:00:00
---

<!-- toc -->
<!-- more -->

# 1. cp命令 复制文件
将文档 file1复制到dir1目录下，复制后名称仍未file1
cp -i file1 dir1

复制目录时，使用-r选项即可递归拷贝，如下：dir1下所有文件包括文件夹，都复制到dir2目录下
cp -r dir1 dir2

参数说明：
`- r` 若源文件是一目录文件，此时cp将递归复制该目录下所有的子目录和文件。当然，目标文件必须为一个目录名。
`- f` 删除已经存在目标文件而不提示。
`- i` 覆盖目标文件前将给出确认提示，属交互式拷贝。

# 2.  rm命令 删除整个文件夹

使用命令 `rm -rf dir1`。若删除时出现 Permission denied 的提示，可以在命令前加sudo 即:`sudo rm -rf dir1`