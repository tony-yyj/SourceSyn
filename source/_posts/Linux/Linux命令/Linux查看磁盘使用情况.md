---
title: Linux查看磁盘使用情况
tags:
  - Linux命令
categories: Linux
date: 2017-09-05 21:18:00
---

<!-- toc -->
<!-- more -->

# 1. 查看磁盘各分区大小、已用空间等信息：

```
df -h
```

# 2. 查看当前目录以下文件和子目录大小 `du -sh * `

```
du -ach *    #这个能看到当前目录下的所有文件占用磁盘大小和总大小
du -sh       #查看当前目录总大小
du -sh *     #查看所有子目录大小
```


du的英文原义为“disk usage”，含义为显示磁盘空间的使用情况，


# 3. 查看所有用户磁盘空间使用情况的shell脚本

## 3.1. 创建test.sh文件

touch homeusage.sh 

## 3.2. 编辑test.sh文件

vi homeusage.sh

## 3.3. 加入内容

```shell
#!/bin/sh  
for user in `ls /home`  
do  
  du -hs "/home/"$user  
done 
#！/bin/bash
```

## 3.4. 保存退出

快捷键Ctrl+C取消输入状态，然后输入 `:wq`

## 3.5. 给test.sh可执行权限

chmod +x homeusage.sh

## 3.6. 执行./test.sh命令

```
mark@mashangxue123.com:~$ touch a.sh
mark@mashangxue123.com:~$ vi a.sh
mark@mashangxue123.com:~$ ./a.sh

root@omnisky:/home/mark# . homeusage.sh
80K	/home/ellie
167G	/home/james
4.5G	/home/mark
17G	/home/omnisky
41M	/home/test1
18M	/home/test2
29M	/home/ubuntu
852M	/home/zhangj
root@omnisky:/home/mark#
```
