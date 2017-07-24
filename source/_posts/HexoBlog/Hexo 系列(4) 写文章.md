---
title: “Hexo 系列(4) 开始写文章”
date: 2017-07-20 19:18:08
tags: 博客
categories: 技术
toc: true
---
创建和发布文章、通过插件在文章内插入图片、普通插入图片、代码样式
<!-- more -->

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

# 文章的模板文件

文章模板，如果你是用 `hexo new post “title”` 新建的文章，那么其实它就是从 `~/blog/scaffolds/post.md`复制了一份到~/blog/source/_posts下，
所以这也意味着你可以直接通过在`~/blog/source/_posts`下新建.md结尾的文件来写新的文章。

但是注意，如果自己直接新建文件，一定要记得加上文件最上方的参数，即下面的相关内容。

关于此模板文件，里面的参数说明参见Hexo官方文档。注意！每一项的:后面均有一个空格

```json
---
title: {{ title }} /*文章标题*/
date: {{ date }} /*日期*/
permalink: /*永久链接，如果设置，且在站点配置文件下的permalink设置了title，则可以替换title*/
categories: /*分类，支持多级，比如：
- technology
- computer
- computer-aided-art
则为technology/computer/computer-aided-art*/
tags: /*标签，多个可以这样写[标签1,标签2,标签3]*/
description: /*描述，加了会在每篇文章的开头显示*/
comments: /*是否开启评论*/
type: /*类型*/
top: /*文章置顶，此项只有参考操作26(http://shenzekun.cn/hexo的next主题个性化配置教程.html)，否则请勿添加*/
password: /*文章密码，此项只有参考操作24(http://shenzekun.cn/hexo的next主题个性化配置教程.html)，否则请勿添加。发现还是有bug的，就是右键在新标签中打开，然后无论是否输入密码，都能看到内容*/
---

```

# 5. 参考文献

[使用github+Hexo人人都能拥有一个美美的博客](http://www.jianshu.com/p/863f3f2d1733)