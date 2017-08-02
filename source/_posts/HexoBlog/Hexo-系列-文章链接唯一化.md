---
title: Hexo 系列 文章链接唯一化
abbrlink: 4036122762
date: 2017-07-26 09:48:42
tags: 
    - Hexo
    - Hexo优化
categories: Hexo
---
也许你会数次更改文章题目或者变更文章发布时间，在默认设置下，文章链接都会改变，不利于搜索引擎收录，也不利于分享。唯一永久链接才是更好的选择。
<!-- more -->
# 1. 方案介绍

对标题+时间进行md5然后再转base64，保存在front-matter中。

首先是注册before_post_render钩子，然后取出来abbrlink这个属性看是否存在，存在的就不管了，否则就生成连接。
其中使用了nodejs自带的crypto模块来获取md5校验值，用hexo-front-matter来转换front-matter，然后用hexo-fs来保存文件。

# 2. 安装插件

```
npm install hexo-abbrlink --save
```
安装后，不要在 hexo s 模式下更改文章文件名，否则文章将成空白。

# 3. 在站点配置文件中 permalink

查找代码 `permalink:`，将其更改为:

```
permalink: posts/:abbrlink/  # “posts/” 可自行更换
```

# 4. 在站点配置文件中添加abbrlink

添加如下代码：

```yml
# abbrlink config
abbrlink:
  alg: crc32  # 算法：crc16(default) and crc32 
  rep: dec    # 进制：dec(default) and hex
```

可参照样例以选择：

```
crc16 & hex
    https://post.zz173.com/posts/66c8.html
crc16 & dec
    https://post.zz173.com/posts/65535.html
crc32 & hex
    https://post.zz173.com/posts/8ddf18fb.html
crc32 & dec
    https://post.zz173.com/posts/1690090958.html

```

# 5. 参考文献

[rozbo/hexo-abbrlink](https://github.com/Rozbo/hexo-abbrlink)
[hexo-abbrlink介绍](https://post.zz173.com/detail/hexo-abbrlink.html)
[Hexo插件之Hexo-UUID](https://chekun.me/post/hexo-uuid/)

[使用 Hexo 搭建博客的深度优化与定制](http://blog.tangxiaozhu.com/p/45374067/)