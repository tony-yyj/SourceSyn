---
title: 自定义Hexo博客的文章模板
abbrlink: 353523292
date: 2017-07-25 16:12:16
tags: 
    - Hexo
    - Hexo优化
categories: Hexo
---
每篇文章源代码的开头部分自定义，博客模版
<!-- more -->
# 1. 博客模版（Scaffold）

scaffolds文件夹：
```
├── scaffolds					//保存着默认模板，自定义模板就是修改该目录下的文件
│   ├── draft.md 				//默认的草稿模板
│   ├── page.md 				//默认的页面模板
│   └── post.md 				//默认的文章模板
```

在新建文章时，Hexo 会根据 scaffolds 文件夹内相对应的文件来建立文件，例如：

```
hexo new photo "My Gallery"
```
在执行这行指令时，Hexo 会尝试在 scaffolds 文件夹中寻找 photo.md，

# 2. 文件的开头

文件的开头是属性（`Front-Matter` ），采用统一的yaml格式，用三条短横线分隔

文章可以拥有如下属性：
- layout  文章的布局，可以取值post（默认值）或page，可以通过修改 _config.yml 中的 default_layout 参数来指定默认布局。
- title	文章的标题
- date	创建日期，文件的创建日期
- updated	修改日期，文件的修改日期
- comments	是否开启评论，默认值true
- tags	标签
- categories	分类
- permalink	url中的名字，默认值文件名


如果你修改了layout，在scaffolds文件夹里一定要有名字对应的模版文件，否则会采用默认模版。

如果你不想你的文章被处理，你可以将 Front-Matter 中的layout: 设为 false 。


# 3. 文件名称

可编辑网站配置文件`_config.yml`中的 new_post_name 参数来改变默认的文件名称，
举例来说，设为 :year-:month-:day-:title.md 可让您更方便的通过日期来管理文章。


[自定义Hexo博客的文章、草稿和页面的模板](http://blog.xinspace.space/2016/04/11/%E8%87%AA%E5%AE%9A%E4%B9%89Hexo%E5%8D%9A%E5%AE%A2%E7%9A%84%E6%96%87%E7%AB%A0%E3%80%81%E8%8D%89%E7%A8%BF%E5%92%8C%E9%A1%B5%E9%9D%A2%E7%9A%84%E6%A8%A1%E6%9D%BF/)