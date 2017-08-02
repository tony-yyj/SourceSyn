---
title: 阿里云虚拟主机 搭建Hexo博客详细步骤
abbrlink: 3927704776
date: 2017-07-27 11:36:38
tags: 
    - Hexo
    - Hexo优化
categories: Hexo
---
<!-- TOC -->

- [1. 注册域名 申请服务器](#1-注册域名-申请服务器)
- [2. 云虚拟主机使用](#2-云虚拟主机使用)
- [3. 网站上传至HTDOCS](#3-网站上传至htdocs)
- [4. 参考文献：](#4-参考文献)

<!-- /TOC -->
<!-- more -->

# 1. 注册域名 申请服务器

上阿里云 万网注册个域名 https://wanwang.aliyun.com/

选一个普惠版云虚拟主机 https://wanwang.aliyun.com/hosting/free/?spm=5176.8060947.436638.1.irgZGN

# 2. 云虚拟主机使用

[云虚拟主机使用手册](https://help.aliyun.com/knowledge_detail/36183.html)


- 第一步   获取主机信息	
- 第二步	网站文件上传、数据库信息上传、网站备案	
- 第三步	网站调试	
- 第四步	域名解析、 网站域名绑定
- 第五步	网站创建成功

# 3. 网站上传至HTDOCS

您的首页文件及网站程序需上传至FTP下的HTDOCS目录下，也就是把Hexo生成的Public文件夹里面的文件上传到htdocs目录
您自行设定的首页文件名，需要添加至控制面板默认首页设置的列表中操作帮助

[云虚拟主机 如何上传网站程序_网站上传/下载](https://help.aliyun.com/knowledge_detail/36241.html)
 
- Windows通过文件浏览器上传网页：输入ftp://您的主机IP地址，并回车，按照要求输入你查到的 主机信息。
- 使用FTP客户端上传文件，无操作系统限制

 虚拟主机不支持远程登录，包括SSH方式，远程桌面RDP方式等。如果您需要远程桌面权限管理，建议您可以 购买服务器 ECS 。

# 4. 参考文献：

[++阿里云虚拟主机+Hexo 零基础搭建个人博客--简单易学 - Royce_he的个人页面](https://my.oschina.net/roycehe/blog/807259)

[+使用 Git Hook 自动部署 Hexo 到个人 VPS](http://www.swiftyper.com/2016/04/17/deploy-hexo-with-git-hook/)

[+阿里云VPS搭建自己的的Hexo博客 - i折腾 - SegmentFault](https://segmentfault.com/a/1190000005723321)

[阿里云搭建Git服务，实现Hexo自动部署](https://imys.net/20160303/hexo-nginx-auto-deploy.html)

[小记 - Hexo 部署到阿里云服务器](http://lijundong.com/note-hexo-deploy-on-server/)

[Mac Hexo + 阿里云同步与自动部署](http://anyang-ai.com/2017/02/10/hexo/)

[如何远程连接阿里云主机服务器(Linux系统）_百度经验](http://jingyan.baidu.com/article/47a29f242b7c0ac014239915.html)

[[网站搭建] 阿里云虚拟主机搭建及FTP文件上传 - Eastmount的专栏 CSDN博客](http://blog.csdn.net/eastmount/article/details/52643702)

[在阿里云部署 Hexo 网站 - Leo的博客- CSDN博客](http://blog.csdn.net/lihao21/article/details/70188750)
