---
title: Hexo插件推荐
abbrlink: 1310093754
date: 2017-07-28 10:52:17
tags: 
    - Hexo
    - Hexo优化
categories: Hexo
---
<!-- TOC -->

- [1. 插件hexo-generator-sitemap 生成网站地图](#1-插件hexo-generator-sitemap-生成网站地图)
    - [1.1. 安装插件命令](#11-安装插件命令)
    - [1.2. 字段配置](#12-字段配置)
- [2. 插件hexo-baidu-url-submit向百度提交链接使用主动推送](#2-插件hexo-baidu-url-submit向百度提交链接使用主动推送)
    - [2.1. 安装插件命令](#21-安装插件命令)
    - [2.2. 字段配置](#22-字段配置)
- [3. 插件hexo-deployer-git 部署到GitHub](#3-插件hexo-deployer-git-部署到github)
    - [3.1. 安装插件命令](#31-安装插件命令)
    - [3.2. 修改站点配置](#32-修改站点配置)
        - [3.2.1. 运行hexo deploy命令](#321-运行hexo-deploy命令)
- [4. 插件hexo-generator-searchdb 使用Local Search本地搜索](#4-插件hexo-generator-searchdb-使用local-search本地搜索)
    - [4.1. 安装插件命令](#41-安装插件命令)
    - [4.2. 编辑 `站点配置`文件](#42-编辑-站点配置文件)
    - [4.3. 编辑 `主题配置`文件](#43-编辑-主题配置文件)
- [5. 插件hexo-abbrlink 文章链接唯一化](#5-插件hexo-abbrlink-文章链接唯一化)
    - [5.1. 安装插件命令](#51-安装插件命令)
    - [5.2. 在站点配置文件中 permalink](#52-在站点配置文件中-permalink)
    - [5.3. 在站点配置文件中添加abbrlink](#53-在站点配置文件中添加abbrlink)
- [6. 插件hexo-asset-image 使用本地图片](#6-插件hexo-asset-image-使用本地图片)
    - [6.1. 安装插件命令](#61-安装插件命令)
    - [6.2. 设定post_asset_folder为true](#62-设定post_asset_folder为true)
    - [6.3. 使用过程](#63-使用过程)
- [7. 添加TOC 目录](#7-添加toc-目录)
    - [7.1. 安装插件命令](#71-安装插件命令)
    - [7.2. 在站点配置文件中添加toc](#72-在站点配置文件中添加toc)
    - [7.3. 使用方法`<!-- toc -->`](#73-使用方法---toc---)
- [8. 参考文献](#8-参考文献)

<!-- /TOC -->
<!-- more -->

# 1. 插件hexo-generator-sitemap 生成网站地图

## 1.1. 安装插件命令

```
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
``` 

## 1.2. 字段配置

在你的站点配置文件中修改 URL 为你的站点地址，
然后在站点配置文件中按如下方式新增字段
```yml
# 自动生成sitemap
sitemap:
  path: sitemap.xml

baidusitemap:
  path: baidusitemap.xml
```
当你在 hexo g 时,会在public文件夹中生成sitemap.xml 和baidusitemap.xml 两个文件。前者适合提交给谷歌搜素引擎，后者适合提交百度搜索引擎


# 2. 插件hexo-baidu-url-submit向百度提交链接使用主动推送

## 2.1. 安装插件命令
```
npm i hexo-baidu-url-submit -S

```

## 2.2. 字段配置

在站点配置文件中按如下方式新增字段
```yml
baidu_url_submit:
  count: 10 # 提交最新的链接数
  host: crowncj.com # 在百度站长平台中注册的域名,虽然官方推荐要带有 www, 但可以不带.
  token:  XXXXX # 你的秘钥,每个人都不一样,获取方法在下面
  path: baidu_urls.txt # 文本文档的地址,新链接会保存在此文本文档里
```
加入新的 deploy,多个 type 的写法,前面那个 type 是推送到 Gitub 与 Coding
```yml
deploy:
 - type: git
   repo:
        github:
        coding:
 - type: baidu_url_submitter
```

最后当你执行hexo d时新的连接就会被推送上去.

# 3. 插件hexo-deployer-git 部署到GitHub

## 3.1. 安装插件命令

```yml
npm install hexo-deployer-git --save 
```

## 3.2. 修改站点配置

文件_config.yml找到以下内容配置

```yml
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  repository: https://github.com/mashangxue/mashangxue.github.io.git
  branch: master
```

### 3.2.1. 运行hexo deploy命令

```
hexo deploy
```
# 4. 插件hexo-generator-searchdb 使用Local Search本地搜索

## 4.1. 安装插件命令

  `npm install hexo-generator-searchdb --save`

## 4.2. 编辑 `站点配置`文件

新增以下内容到任意位置 

```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

## 4.3. 编辑 `主题配置`文件

启用本地搜索功能 

```
# Local search
local_search:
  enable: true
```

# 5. 插件hexo-abbrlink 文章链接唯一化

## 5.1. 安装插件命令

对标题+时间进行md5然后再转base64，保存在front-matter中。

```
npm install hexo-abbrlink --save
```
安装后，不要在 hexo s 模式下更改文章文件名，否则文章将成空白。

## 5.2. 在站点配置文件中 permalink

查找代码 `permalink:`，将其更改为:

```
permalink: posts/:abbrlink/  # “posts/” 可自行更换
```

## 5.3. 在站点配置文件中添加abbrlink

添加如下代码 

```yml
# abbrlink config
abbrlink:
  alg: crc32  # 算法 crc16(default) and crc32 
  rep: dec    # 进制 dec(default) and hex
```

# 6. 插件hexo-asset-image 使用本地图片

这个插件在使用本地图片的时候很是方便，图片只需要放在文章同名文件夹中即可，然后文章的引用路径就是简单的文章名（就是图片的文件夹名）/图片名。

## 6.1. 安装插件命令

```
npm install hexo-asset-image --save
或者
npm install https://github.com/CodeFalling/hexo-asset-image --save
```

## 6.2. 设定post_asset_folder为true

确认根目录站点配置文件 `_config.yml`中有`post_asset_folder: true`。

Hexo提供了一种更方便管理Asset的设定 post_asset_folder
当您设置post_asset_folder为true参数后，在建立文件时，Hexo会自动建立一个与文章同名的文件夹；以前的文章也可以自己手动创建同名文件夹。

## 6.3. 使用过程

完成安装后用hexo新建文章的时候会发现_posts目录下面会多出一个和文章名字一样的文件夹，图片就可以放在文件夹下面。
新建文章结构如下 

```
本地图片测试
├── logo.jpg
本地图片测试.md
```

利用makdown插入图片 其中[]里面不写文字则没有图片标题。记住仅仅使用文件名就可以，不用带路径。


```
![](logo.jpg)
```

利用标签引用 
[资源文件夹](https://hexo.io/zh-cn/docs/asset-folders.html)

```
 {% asset_path slug %}
 {% asset_img slug [title] %}
 {% asset_link slug [title] %}
```

注意:
通过常规的 markdown 语法和相对路径来引用图片和其它资源可能会导致它们在**存档页或者主页**上显示不正确。

比如说 当你打开文章资源文件夹功能后，你把一个 `example.jpg`图片放在了你的资源文件夹中，
如果通过使用相对路径的常规 markdown 语法 `[](/example.jpg)`，它将 不会出现在首页上。（但是它会在文章中按你期待的方式工作）

正确的引用图片方式是使用下列的标签插件而不是markdown

```
{% asset_img example.jpg This is an example image %}
```
通过这种方式，图片将会同时出现在文章和主页以及归档页中。


最终网站的结构为

```
public/2017/07/9/本地图片测试
                ├── index.html
                ├── logo.jpg
```

同时，生成的 html 是

```html
<img src="/2017/07/9/本地图片测试/logo.jpg" alt="logo">
```

# 7. 添加TOC 目录

## 7.1. 安装插件命令
```
npm install hexo-toc --save

```

## 7.2. 在站点配置文件中添加toc

```yml
toc:
  maxdepth: 3
  class: toc
  slugify: transliteration
  anchor:
    position: after
    symbol: '#'
    style: header-anchor
```

## 7.3. 使用方法`<!-- toc -->`

使用的时候，只需要添加 
```
<!-- toc -->
```

# 8. 参考文献 

[hexo博客图片问题](http://www.jianshu.com/p/950f8f13a36c)

[Hexo 博客从搭建部署到SEO优化等详细教程](http://www.jianshu.com/p/efaf72aab32e)
[ Hexo七牛图床使用 - Roylee Blog From A iOS Developer ](http://error408.com/2016/08/02/Hexo%E4%B8%83%E7%89%9B%E5%9B%BE%E5%BA%8A%E4%BD%BF%E7%94%A8/)