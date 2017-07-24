---
title: “Hexo 系列(2) 博客配置”
date: 2017-07-20 15:15:04
tags: 博客
categories: 技术
toc: true
---
<!-- TOC -->

- [1. 添加菜单栏](#1-添加菜单栏)
    - [1.1. 添加字段](#11-添加字段)
    - [1.2. 更新字符串](#12-更新字符串)
    - [1.3. about目录](#13-about目录)
- [2. 标签目录](#2-标签目录)
    - [2.1. 站点配置](#21-站点配置)
    - [2.2. 主题配置](#22-主题配置)
    - [2.3. 新建tags页面](#23-新建tags页面)
    - [2.4. 修改tags的名字](#24-修改tags的名字)
    - [2.5. 在文章中添加tags](#25-在文章中添加tags)
- [3. 分类](#3-分类)
    - [3.1. 站点配置文件](#31-站点配置文件)
    - [3.2. 主题配置文件](#32-主题配置文件)
    - [3.3. 新建categories文件](#33-新建categories文件)
    - [3.4. 修改categories/index.md](#34-修改categoriesindexmd)
    - [3.5. 在文章中添加categories](#35-在文章中添加categories)
- [4. 添加sitemap和feed插件](#4-添加sitemap和feed插件)

<!-- /TOC -->
# 1. 添加菜单栏

## 1.1. 添加字段
进入theme目录，编辑_config_yml文件，找到menu:字段，在该字段下添加一个字段。

```
menu:
  home: /
  about: /about
  ......
```

## 1.2. 更新字符串
进入 lanhuages 目录，编辑zh-Hans.yml文件，更新页面要显示的中文字符，

```
menu:
  home: 首页
  about: 关于作者
  ......
```

## 1.3. about目录

进入theme目录下的Source目录，新增一个about目录，里面写一个index.html文件。


# 2. 标签目录

## 2.1. 站点配置
文件中有  `tag_dir: tags`

## 2.2. 主题配置
文件中有 `tags: tags`

## 2.3. 新建tags页面

命令 `$ hexo new page tags`  此时会在source/ 下生成 `tags/index.md`文件

## 2.4. 修改tags的名字

```
title: tags
date: 2017-07-20 10:10:10
type: "tags"
comments: false
```

## 2.5. 在文章中添加tags

在文章xx.md中添加：

```
title: TagEditText
date: 2017-07-20 10:10:10
tags: 
	- Tag1
	- Tag2
	- Tag3
```

# 3. 分类

## 3.1. 站点配置文件
打开了 `category_dir: categories`

## 3.2. 主题配置文件
打开了 `categories: /categories`

## 3.3. 新建categories文件

命令 `$ hexo new page categories`  此时会在source目录下生成 `categories/index.md` 文件

## 3.4. 修改categories/index.md

```
title: categories
date: 2017-07-20 10:10:10
type: "categories"
comments: false
```

## 3.5. 在文章中添加categories 
在文章xx.md中添加：

```
title: TagEditText
date: 2016-11-19 10:44:25
categories: 
	- cate
```

# 4. 添加sitemap和feed插件

```
$ npm install hexo-generator-feed
$ npm install hexo-generator-sitemap
```

修改_config.yml，增加以下内容

```
//# Extensions
Plugins:
- hexo-generator-feed
- hexo-generator-sitemap
//#Feed Atom
feed:
  type: atom
  path: atom.xml
  limit: 20
//#sitemap
sitemap:
  path: sitemap.xml
```  
配完之后，atom.xml和sitemap.xml这两个文件成功生成了。