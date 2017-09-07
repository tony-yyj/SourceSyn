---
title: Linux查看磁盘使用情况
tags:
  - Linux命令
categories: Linux
abbrlink: 1070661370
date: 2017-09-05 21:18:00
---

<!-- toc -->
<!-- more -->

# 1. 查看磁盘各分区大小、已用空间等信息：

```
df -h
```
效果演示：

```bash
mark@mashangxue123.com:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            252G     0  252G   0% /dev
tmpfs            51G   11M   51G   1% /run
/dev/sda3       226G  213G  1.3G 100% /
tmpfs           252G  108K  252G   1% /dev/shm
tmpfs           5.0M  4.0K  5.0M   1% /run/lock
tmpfs           252G     0  252G   0% /sys/fs/cgroup
/dev/sda1       188M  3.5M  184M   2% /boot/efi
tmpfs            51G   24K   51G   1% /run/user/108
/dev/sdb1       3.6T   29G  3.4T   1% /disk1
/dev/sdc1       3.6T   68M  3.4T   1% /disk2
tmpfs            51G     0   51G   0% /run/user/1000
tmpfs            51G     0   51G   0% /run/user/1007
```

# 2. 查看当前目录以下文件和子目录大小 `du -sh * `

```
du -ach *    #这个能看到当前目录下的所有文件占用磁盘大小和总大小
du -sh       #查看当前目录总大小
du -sh *     #查看所有子目录大小
```
du的英文原义为“disk usage”，含义为显示磁盘空间的使用情况，

举例：
**对根目录下文件夹进行大小排序**
切到根目录下，使用以下命令进行排序：
```
du -h --max-depth=1|grep G|sort -n 
```

[/proc目录造成linux根目录爆满_百度经验](http://jingyan.baidu.com/article/454316ab733e1ef7a6c03a71.html)

# 3. 区别df和du

du -Disk Usage

df -Disk Free

du估计文件空间占用情况，df报告文件系统磁盘空间使用情况

[df和du显示的磁盘空间使用情况不一致的原因及处理 - 夏雪冬日 - 博客园](http://www.cnblogs.com/heyonggang/p/3644736.html)

# 4. 查看所有用户磁盘空间使用情况的shell脚本

## 4.1. 创建test.sh文件

touch homeusage.sh 

## 4.2. 编辑test.sh文件

vi homeusage.sh

## 4.3. 加入内容

```shell
#!/bin/sh  
for user in `ls /home`  
do  
  du -hs "/home/"$user  
done 
#！/bin/bash
```

## 4.4. 保存退出

快捷键Ctrl+C取消输入状态，然后输入 `:wq`

## 4.5. 给homeusage.sh可执行权限

chmod +x homeusage.sh

## 4.6. 执行./homeusage.sh命令

```
mark@mashangxue123.com:~$ touch homeusage.sh
mark@mashangxue123.com:~$ vi homeusage.sh
mark@mashangxue123.com:~$ ./homeusage.sh

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
