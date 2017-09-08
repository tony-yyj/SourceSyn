---
title: 如何下载SlideShare的PPT
tags:
  - PPT
categories: note
abbrlink: 3436209124
date: 2017-09-08 21:30:00
---
<!-- toc -->
<!-- more -->
# 1. 把网址复制到这个网站就可以生成下载地址

http://grub.cballenar.me/


SlideShare中有很多不错的PPT，有时候确实想收藏怎么办，通常有2种方法：

# 2. SWF档案的PPT

A. 打开PPT首页，按ctrl+U打开源码
B. 找到类似以下语法的语句：

```
<meta name="thumbnail" content="http://cdn.slidesharecdn.com/ss_thumbnails/2013-09-28-user-experience-crossroads-130929220129-phpapp01-thumbnail.jpg?cb=1381014525"/>
```

C. 删除“-thumbnail.jpg?cb=1381014525"/>” 和“ss_thumbnails”
D. 在浏览器中输入剩下的地址：

http://cdn.slidesharecdn.com/2013-09-28-user-experience-crossroads-130929220129-phpapp01
E. 下载页面中出现的全部swf档即可

# 3. JPG档案的PPT

还有一种PPT不是SWF格式的，是JPG转成PDF格式的，那么上述方法就无效了，需要这么做：

A. ctrl+U打开源码
B. 找到

<div class="slide_container">

C. 将它下面的代码copy到文本编辑器中
D. 用replace大法去掉杂七杂八的东西，剩下原始地址
E. 用迅雷批量下载即可

[如何下载SlideShare的PPT：2种方法 - o0松鼠0o - 博客园](http://www.cnblogs.com/x5115x/p/4908577.html)
[【分享】SlideShare檔案下載的方法教學，一鍵將整份簡報儲存到電腦。 | Techmarks劃重點](https://www.techmarks.com/slideshare-downloader/#SlideGrubber)