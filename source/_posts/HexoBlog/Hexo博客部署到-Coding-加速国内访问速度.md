---
title: Hexo博客部署到 Coding 加速国内访问速度
tags:
  - Hexo
  - Hexo优化
categories: Hexo
abbrlink: 3503968978
date: 2017-07-29 17:54:31
alias: 3503968978/
---
Hexo博客 Coding部署
<!-- TOC -->

- [1. 创建项目并设置为Pages服务](#1-创建项目并设置为pages服务)
- [2. ssh对接对接 方便上传](#2-ssh对接对接-方便上传)
    - [2.1. 用git bash输入命令](#21-用git-bash输入命令)
    - [2.2. 查看ssh命令：](#22-查看ssh命令)
    - [2.3. 在coding添加ssh](#23-在coding添加ssh)
- [3. hexo配置](#3-hexo配置)

<!-- /TOC -->
<!-- more -->

# 1. 创建项目并设置为Pages服务

# 2. ssh对接对接 方便上传

## 2.1. 用git bash输入命令
```
ssh-keygen
```
一直按回车键，直到结束。

## 2.2. 查看ssh命令：
```
cat ~/.ssh/id_rsa.pub
```
复制输出的全部内容。

## 2.3. 在coding添加ssh

在coding的个人页面，找到SSH公钥，添加，粘贴上面复制的公钥。

# 3. hexo配置

新建好了coding的项目之后，修改一下站点的配置文件，_config.yml如下:
```yml
# Deployment 部署配置，将本地public目录也就是网站部署到服务器上的配置
## Docs: https://hexo.io/docs/deployment.html
deploy:
  - type: git
    repo: 
      github: https://github.com/mashangxue/mashangxue.github.io.git
      coding: https://git.coding.net/mashangxue/mashangxue.git
    branch: master
  #- type: baidu_url_submitter
```
由于的都是master分支，所以两个写到一起了，如果不是同一个分支的话，可以如下的写法：

```yml
deploy:
  type: git
  repository:
      github: git@github.com:mashangxue/mashangxue.github.io.git,分支名称
      coding: git@git.coding.net:mashangxue/mashangxue.git,分支名称
```

现在可以deploy 部署了

```
$ hexo clean
$ hexo g
$ hexo d
```

参考文献：
[hexo同时部署到coding(gitcafe)和github](http://shomy.top/2016/03/03/hexo-in-coding-github/)

[hexo博客添加域名实现双线部署（github和coding） - CSDN博客](http://blog.csdn.net/qiuchengjia/article/details/52923156)