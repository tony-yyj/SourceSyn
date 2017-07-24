---
title: “Hexo 系列(1) 搭建个人博客”
date: 2017-07-20 15:15:04
tags: 博客
categories: 技术
---
<!-- TOC -->

- [1. 准备工作](#1-准备工作)
    - [1.1. 安装node.js](#11-安装nodejs)
    - [1.2. 安装git](#12-安装git)
    - [1.3. 安装hexo](#13-安装hexo)
- [2. 开始搭建博客](#2-开始搭建博客)
    - [2.1. hexo创建一个目录](#21-hexo创建一个目录)
    - [2.2. 生成静态页面](#22-生成静态页面)
    - [2.3. 本地运行](#23-本地运行)
    - [2.4. 看效果](#24-看效果)
    - [2.5. Hexo常用的几个命令](#25-hexo常用的几个命令)
- [3. 网站配置](#3-网站配置)
- [4. 发一篇文章](#4-发一篇文章)
- [5. 换为next主题](#5-换为next主题)
    - [5.1. 下载主题](#51-下载主题)
    - [5.2. 网站配置要使用的主题](#52-网站配置要使用的主题)
    - [5.3. 主题的配置](#53-主题的配置)
- [6. 部署到Github](#6-部署到github)
    - [6.1. 申请一个github账号](#61-申请一个github账号)
    - [6.2. 创建一个仓库](#62-创建一个仓库)
    - [6.3. 安装 hexo-deployer-git](#63-安装-hexo-deployer-git)
    - [6.4. 网站配置deploy](#64-网站配置deploy)
    - [6.5. 部署](#65-部署)
    - [6.6. 效果](#66-效果)
- [7. 绑定域名](#7-绑定域名)
    - [7.1. 域名提供商设置](#71-域名提供商设置)
    - [7.2. 博客添加CNAME文件](#72-博客添加cname文件)
    - [7.3. 查看效果](#73-查看效果)
- [8. 更新文章](#8-更新文章)
- [9. 博客源码管理](#9-博客源码管理)
- [10. 参考文献](#10-参考文献)

<!-- /TOC -->

# 1. 准备工作

## 1.1. 安装node.js

[nodejs官网 https://nodejs.org/en/download/](https://nodejs.org/en/download/)

检验安装成功： `$ node -v`

## 1.2. 安装git

## 1.3. 安装hexo

方法：打开cmd 运行`$ npm install hexo-cli -g`（要翻墙，可以切换到淘宝镜像 http://npm.taobao.org/ ）

npm install  安装时报错，可能是国内网络问题，请尝试使用代理或者切换至淘宝NPM镜像安装：

Mac系统，则需要 `$ sudo npm install hexo-cli -g`

# 2. 开始搭建博客

## 2.1. hexo创建一个目录

用命令创建 `myblog`

```
hexo init myblog
cd myblog
npm install

```

## 2.2. 生成静态页面

```
$ hexo g
```
(g 即generate)

## 2.3. 本地运行

运行 `$ hexo s`(s 即server)

## 2.4. 看效果

打开浏览器，输入地址 `http://localhost:4000/` 即可

## 2.5. Hexo常用的几个命令

hexo generate (hexo g) 生成静态文件，会在当前目录下生成一个新的叫做public的文件夹
hexo server (hexo s) 启动本地web服务，用于博客的预览
hexo deploy (hexo d) 部署博客到远端（比如github, heroku等平台）

hexo new "postName" #新建文章
hexo new page "pageName" #新建页面

# 3. 网站配置

网站的配置大部分都在**_config.yml**文件中，详细配置可以查看官方文档

下面是常用配置：

- title -> 网站标题
- subtitle -> 网站副标题
- description -> 网站描述
- author -> 您的名字
- language -> 网站使用的语言

注意：进行配置时，需要在冒号:后加一个英文空格。

语言文件并放在主题文件夹中的 languages 文件夹，这里填文件夹名字。

# 4. 发一篇文章

命令 `$ hexo new test` 生成文章。  此时会在 `source/_posts`目录下生成`test.md`文件.

命令`hexo g`生成静态网页, `hexo s` 本地看效果

# 5. 换为next主题

## 5.1. 下载主题

命令： `$ git clone https://github.com/iissnan/hexo-theme-next  themes/next`

## 5.2. 网站配置要使用的主题

在网站配置文件**_config.yml**中，配置**theme**

修改这行： `theme: next`    next是主题名称

## 5.3. 主题的配置

可在主题自己的配置文件 `/theme/next/_config.yml` 下进行主题的配置。

执行调试命令看看效果
```
$ hexo clean
$ hexo g
$ hexo s
```

# 6. 部署到Github

## 6.1. 申请一个github账号

账号名自己取，这里使用mashangxue代替

## 6.2. 创建一个仓库

命名`mashangxue.github.io` ，一定要把你的账号名字加入到仓库名

## 6.3. 安装 hexo-deployer-git

 运行命令`$ npm install hexo-deployer-git --save`

## 6.4. 网站配置deploy

 在网站的 `_config.yml`文件中配置deploy
```bash
deploy:
  type: git
  repo: https://github.com/mashangxue/mashangxue.github.io.git
  branch: master
```

branch为分支，默认为master,

## 6.5. 部署

运行：`hexo g`（本地生成静态文件）
运行：`hexo d`（将本地静态文件推送至Github）

## 6.6. 效果

打开浏览器，访问http://mashangxue.github.io

# 7. 绑定域名

博客已经搭建好，也能通过github的域名访问，我们希望将自己的域名绑定到这个博客项目上。

GitLab Pages可以绑定域名，而且可以上传自定义SSL证书，比如CloudFlare的免费SSL证书。

## 7.1. 域名提供商设置

添加2条A记录：

```
@—>192.30.252.154

@—>192.30.252.153
```

添加一条CNAME记录： `CNAME—> mashangxue.github.io`

## 7.2. 博客添加CNAME文件

在source目录下新建 一个命名 `CNAME` 的文件，写入域名，如：`www.mashangxue123.com`

## 7.3. 查看效果

运行：hexo g

运行：hexo d

打开浏览器，访问 `http://www.mashangxue123.com/`

# 8. 更新文章

在MyBlog目录下执行：`hexo new “我的第一篇文章”` ，会在source->_posts文件夹内生成一个.md文件。

编辑该文件（遵循Markdown规则）修改起始字段:
- title 文章的标题
- date 创建日期 （文件的创建日期 ）
- updated 修改日期 （ 文件的修改日期）
- comments 是否开启评论 true
- tags 标签
- categories 分类
- permalink url中的名字（文件名）
- 编写正文内容（MakeDown）

生成网页：
- hexo clean 删除本地静态文件（Public目录），可不执行。
- hexo g 生成本地静态文件（Public目录）
- hexo deploy 将本地静态文件推送至github（hexo d）

# 9. 博客源码管理

在GitHub上搭建Hexo博客只能本地渲染成HTML文件，然后hexo d把渲染后的文件push到repo。
如果需要管理博客源文件就需要新建一个repo，或者新建一个分支管理博客源代码。

一般都采取双分支策略：master分支用于发布渲染后的html，自己在建立一个hexo分支保存md原文件，这样每次只需要在hexo分支工作，发布的时候自动deploy到master分支。

# 10. 参考文献

[有哪些好看的 Hexo 主题？ - 知乎](https://www.zhihu.com/question/24422335/answers/created)

[Hexo](https://hexo.io/)

[GitLab Pages搭建Hexo博客](https://www.ouyangsong.com/2017/05/28/gitlab-pages-hexo-cloudflare-ssl-markdown/)

[【置顶】Hexo搭建博客教程](https://thief.one/2017/03/03/Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E6%95%99%E7%A8%8B/)

[++ Hexo 博客搭建指南limedroid/HexoLearning](https://github.com/limedroid/HexoLearning)

[手把手教你使用Hexo + Github Pages搭建个人独立博客](https://linghucong.js.org/2016/04/15/2016-04-15-hexo-github-pages-blog/)
