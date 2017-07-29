---
title: Hexo 目录介绍
abbrlink: 2286160507
date: 2017-07-25 16:37:57
tags: 
    - Hexo
categories: Hexo搭建博客
---
Hexo目录中每个文件用途介绍
<!-- more -->
```
├── .deploy
├── public
├── scaffolds
├── scripts
├── source
|   ├── _drafts
|   └── _posts
├── themes
├── _config.yml
└── package.json
```

- deploy： 执行 `hexo deploy`命令部署到GitHub上的内容目录
- public： 执行 `hexo generate`命令，输出的静态网页内容目录
- scaffolds：layout模板文件目录，其中的md文件可以添加编辑
- scripts： 扩展脚本目录，这里可以自定义一些javascript脚本
- source： 文章源码目录，该目录下的markdown和html文件均会被hexo处理。该页面对应repo的根目录，404文件、favicon.ico文件，CNAME文件等- 都应该放这里，该目录下可新建页面目录。
-         _drafts：草稿文章
-         _posts： 发布文章
- themes：  主题文件目录
- _config.yml： 全局配置文件，大多数的设置都在这里
- package.json：应用程序数据，指明hexo的版本等信息，类似于一般软件中的关于按钮

