---
title: Hexo 插入图片的几种方法
tags: []
categories: []
abbrlink: 1322489026
abbrlinkurl: '原文 http://www.mashangxue123.com/1322489026'
date: 2017-08-01 15:39:23
---

222

33333378
![](2614392944_output_1_0.png)

33333378
![](2614392944_output_1_0.png)

aaaaa

{% imgurl 2614392944_output_1_0.png full-image alt:test title:test %}

{% asset_img example.jpg This is an example image %}


Hexo 支持更使用特定的语法，插入指定大小的图片，如下：

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
- 路径是相对于 conifg 内的 root 的，这一点挺坑，可以在 source/ 下新建一个 uploads 文件夹用于专门放置这些图片资源
```
{\% img hi /uploads/images/test.jpg 100 100 hello hello %}

```
- 图片宽高只能使用数值，不能包含字符串，也不能是百分数
- 最后一个字段可以为图片添加标题


[Hexo 文章图片管理](https://rainylog.com/post/hexo-post-image-manage/)

[资源文件夹 标签](https://hexo.io/zh-cn/docs/asset-folders.html)

[为 Hexo 主题添加多种图片样式](http://wuchong.me/blog/2014/12/13/hexo-theme-creating-image-styles/)
[使用 Hexo 与 NexT 搭建博客的避坑总结](http://yangfch3.com/2016/05/08/hexo-experiences/)