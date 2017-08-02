---
title: Hexo 插入图片的几种方法
tags: [Hexo]
categories: Hexo
abbrlink: 1322489026
abbrlinkurl: '原文 http://www.mashangxue123.com/1322489026'
date: 2017-08-01 15:39:23
---

<!-- toc -->
<!-- more -->

# 1. 传统Markdown方式

在主题的 source 下面新建一个 文件夹（比如uploads）用于专门放置这些图片资源。

使用的时候使用```![](/uploads/test.jpg)```的方式。

# 2. Hexo方式post_asset_folder

- 根目录下的配置文件_config.yml里的post_asset_folder选项设置为true。新建文章的时候会同时创建一个同名文件夹用于放图片。

- 执行命令`npm install hexo-asset-image --save` ，下载安装一个可以上传本地图片的插件：

- 使用的时候，只需要图片名就可以 ``` ![](test.jpg)```

- 也可以使用Hexo推荐的标签方式 ``` {% asset_img example.jpg This is an example image %}```

# 3. 网络图片插入

可以把你的图片上传到 七牛之类的服务器，然后直接按照markdown的方式使用。

# 4. 其他语法

Hexo 支持使用特定的语法，插入指定大小的图片，如下：

```js
// 语法
{% img [class names] /path/to/image [width] [height] [title text [alt text]] %}
// 实例
{% img full-image /hexo-experiences/PL01.jpg 180 180 hello %}
// 生成的代码
<img src="/blog/hexo-experiences/PL01.jpg" class="full-image" width="180" height="180" title="hello">

```
值的注意的几点：

- 路径名必须以 / 开始，否则会解析出错
- 路径是相对于 conifg 内的 root 的

# 5. 参考文献

[Hexo 文章图片管理](https://rainylog.com/post/hexo-post-image-manage/)

[资源文件夹 标签](https://hexo.io/zh-cn/docs/asset-folders.html)

[为 Hexo 主题添加多种图片样式](http://wuchong.me/blog/2014/12/13/hexo-theme-creating-image-styles/)

[使用 Hexo 与 NexT 搭建博客的避坑总结](http://yangfch3.com/2016/05/08/hexo-experiences/)

[hexo博客中如何插入图片](https://univer2012.github.io/2017/04/23/6how-to-insert-picture-in-hexo-blog/)

[Hexo博客搭建之在文章中插入图片](https://yanyinhong.github.io/2017/05/02/How-to-insert-image-in-hexo-post/)