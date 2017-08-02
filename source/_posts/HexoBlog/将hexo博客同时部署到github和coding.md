---
title: 将hexo博客同时部署到github和coding
abbrlink: 1174015716
date: 2017-07-27 14:15:45
tags: 
    - github
    - Hexo
categories: Hexo
---
本篇主要讲一下具体应该怎么配置才能实现hexo静态博客github coding双线部署，通过域名解析（万网 DNSpod）实现国内用户访问coding服务器，国外用户访问github服务器。
<!-- more -->
# 1. 配置hexo的_config文件

具体配置格式如下：

```yml
deploy:
  type: git
  repo:
        github: git@github.com:mashangxue/mashangxue.github.io.git,master
        coding: git@git.coding.net:mashangxue/mashangxue.git,coding-pages

```
这样在执行hexo deploy命令时就会同时部署到github和coding，由于之前已经配置了ssh，所以这里并不需要输密码 非常方便。


# 2. 绑定自己的域名并进行域名解析的配置

## 2.1. 购买域名

域名可以从阿里云的万网购买的，大家也可以去GoDaddy（音译名：狗爹）口碑也不错。

万网 https://wanwang.aliyun.com/ 

## 2.2. 域名解析的配置

直接点进入高级设置：
将coding的地址设置为默认，将github的地址设为海外，点击主机记录可以在下面看到@及www等的区别。@表示不带WWW的网址。


# 3. 在coding和github绑定自己的域名

## 3.1. github绑定

在Hexo的source文件夹新建一个CNAME文件，文件里面写上你的域名，格式如下（不加www）：
`mashangxue123.com`

然后按照部署流程，将更改部署到github就可以了，部署完你就会看到在github项目根目录下看到这个CNAME文件，github就会根据这个文件把github page绑定到设置域名，值得注意的是CNAME文件只能写一个域名，写多个的话也只能识别一个。

## 3.2. coding绑定

coding可以绑定多个域名，并且不用手动添加CNAME文件，直接登录coding设置就好了
具体步骤：
进入项目->点击左侧的代码->然后点击Pages 服务->输入域名->点击添加域名绑定

参考文献：
[hexo同时部署到coding(gitcafe)和github](http://shomy.top/2016/03/03/hexo-in-coding-github/)
[hexo博客添加域名实现双线部署（github和coding）- CSDN博客](http://blog.csdn.net/qiuchengjia/article/details/52923156)
[将hexo博客部署到coding.net](http://www.ieclipse.cn/2016/09/08/Web/hexo-coding-pages/index.html#部署验证)
[将hexo博客到同时部署到github和coding 实现全球快速访问 ](http://xiaobin.me/2016/06/01/github-coding-deploy/)