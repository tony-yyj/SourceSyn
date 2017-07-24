---
title: “Hexo 系列(4) 开始写文章”
date: 2017-07-20 15:15:04
tags: 博客
categories: 技术
toc: true
---
<!-- TOC -->

- [1. 创建和发布文章](#1-创建和发布文章)
- [2. 通过插件在文章内插入图片](#2-通过插件在文章内插入图片)
- [3. 普通插入图片](#3-普通插入图片)
- [4. 代码样式](#4-代码样式)
- [5. 参考文献](#5-参考文献)

<!-- /TOC -->

# 1. 创建和发布文章

创建命令 `hexo new "文章标题"`
文章写好直接执行下面命令即可直接发布文章  ```hexo d -g```

# 2. 通过插件在文章内插入图片

文章插入图片需要用到Hexo的一个插件，首先cd到hexo的根目录

`npm install https://github.com/CodeFalling/hexo-asset-image --save`

然后把图片放入对应文章的配套文件夹下，比如1.png  ```![](github-hexo-blog/1.png)```

# 3. 普通插入图片

在文章中写入:

![](/upload_image/1.jpg)

　　然后进入themes-主题名-> source-> upload_image 目录下(自己创建)，将图片放到这个目录下，就可以了。

说明：当执行hexo g命令时，会自动把图片复制到 public文件的upload_image目录下。

# 4. 代码样式

样式不好看，你可以下载别的主题，替换代码显示样式文件

文件地址 `/source/css/_partial/highlight.styl`

# 5. 参考文献
[使用github+Hexo人人都能拥有一个美美的博客](http://www.jianshu.com/p/863f3f2d1733)