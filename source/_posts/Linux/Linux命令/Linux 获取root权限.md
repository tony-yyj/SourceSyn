---
title: Linux 获取root权限
tags:
  - Linux命令
categories: Linux
abbrlink: 914414906
date: 2017-09-06 19:00:00
---

<!-- toc -->
<!-- more -->


1.输入 `sudo  passwd root` 并设置密码

2.输入 `su root `

示例：
```
mark@mashangxue123.com:~$ su root
Password: 
su: Authentication failure
mark@mashangxue123.com:~$ sudo  passwd root
[sudo] password for mark: 
Enter new UNIX password: 
Retype new UNIX password: 
passwd: password updated successfully
mark@mashangxue123.com:~$ su root
Password: 
root@omnisky:/home/mark# 

```