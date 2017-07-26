---
title: Hexo 系列之 _config.yml站点配置文件
abbrlink: 982564298
date: 2017-07-25 17:17:34
tags:
categories:
---
博客根目录下_config.yml站点配置文件。
<!-- more -->

# 文件内容详细介绍：

```yml
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
# 站点名字，也就是html的title，会显示在浏览器标签上。
title: 马上学
# 站点副标题，会显示在首页上，可以不填。
subtitle: 一切就是这么简单
description:
# 站点描述，可以不填。
author: Markmin
# 语言
language: zh-Hans
# 站点时区，默认是电脑时间
timezone:

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
# 站点网址
# 如果网址是次级目录，比如：http://example.com/blog，
# 那么就要设置`url`为`http://example.com/blog`，并且`root`要设置为`/blog/`
url: http://www.mashangxue123.com/
# 站点根目录
root: /
# 文章的永久网址链接，默认是:year/:month/:day/:title/，。
permalink: :year/:month/:day/:title/
permalink_defaults:

# 目录配置：
# Directory
source_dir: source
#  public目录，静态网站生成的地方，默认值为public
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
# 不想被渲染的路径
skip_render: baidu_verify_j461ONwJ3o.html

# 写作配置
# Writing
# 新建文章默认文件名
new_post_name: :year-:month-:day-:title.md # File name of new posts
# 默认布局
default_layout: post
titlecase: false # Transform title into titlecase
# 在新标签中打开一个外部链接，默认为true
external_link: true # Open external links in new tab
# 转换文件名，1代表小写；2代表大写；默认为0，意思就是创建文章的时候，是否自动帮你转换文件名，默认就行，
filename_case: 0
# 是否渲染_drafts目录下的文章，默认为false
render_drafts: false
# 是否启用Asset Folder，默认为false
post_asset_folder: false
relative_link: false
# 是否显示未来日期文章，默认为true
future: true
# 代码块设置
highlight:
  enable: true
  line_number: true
  auto_detect: true #代码自动高亮
  tab_replace:
  
# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10
  order_by: -date
  
# Category & Tag分类和标签的设置：
# 默认分类，默认为无分类，当然你可以设置一个默认分类。
default_category: uncategorized
category_map:
tag_map:

# Date / Time format日期和时间格式配置：
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss

# Pagination 分页设置：
## Set per_page to 0 to disable pagination
# 一页显示多少篇文章，0 为不分页，默认值为 10
per_page: 15
# 分页目录，默认值为page
pagination_dir: page

# Extensions 扩展配置：
## Plugins: https://hexo.io/plugins/
Plugins:
- hexo-generator-sitemap
#- hexo-generator-feed

# Feed Atom
#feed:
#  type: atom
#  path: atom.xml
#  limit: 20


# 自动生成sitemap
sitemap:
  path: sitemap.xml

baidusitemap:
  path: baidusitemap.xml

search:
  path: search.xml
  field: post
  format: html
  limit: 10000

## Themes: https://hexo.io/themes/主题配置
# maupassant  next yilia jacman
theme: next

# Deployment 部署配置，将本地public目录也就是网站部署到服务器上的配置
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/mashangxue/mashangxue.github.io.git
  branch: master

```

# 配置分了几个大块

## （1）站点参数设置：

- title 站点名字，也就是html的title，会显示在浏览器标签上。
- subtitle 站点副标题，会显示在首页上，可以不填。
- description 站点描述，可以不填。
- author 作者
- language 语言
- timezone 站点时区，默认是电脑时间

## （2）URL设置：

- url 站点网址
- root 站- 点根目录
- permalink 文章的永久网址链接，默认是:year/:month/:day/:title/
- permalink_default
如果网址是次级目录，比如：http://example.com/blog，那么就要设置`url`为`http://example.com/blog`，并且`root`要设置为`/blog/`。

## （3）目录配置：

- source_dir source目录，默认值为source
- public_dir public目录，静态网站生成的地方，默认值为public
- tag_dir tag目录
- archive_dir Archive目录
- category_dir 分类目录
- code_dir 代码目录
- i18n_dir i18n目录
- skip_render 不想被渲染的路径
上面这一部分的值，默认的就行了。

## （4）写作配置：

- new_post_name 新建文章默认文件名，默认值为 :title.md，比如你执行命令hexo new hello，就会默认在_post目录下创建一个hello.md的文件。
- default_layout 默认布局
- titlecase
- external_link 在新标签中打开一个外部链接，默认为true
- filename_case 转换文件名，1代表小写；2代表大写；默认为0，意思就是创建文章的时候，是否自动帮你转换文件名，默认就行，意义不大。
- render_drafts 是否渲染_drafts目录下的文章，默认为false
- post_asset_folder 是否启用Asset Folder，默认为false，至于什么是Asset Folder，后面有讲解。
- future 是否显示未来日期文章，默认为true
- highlight 代码块设置

这一部分也可以基本不变，默认值就行。

## （5）分类和标签的设置：

- default_category 默认分类，默认为无分类，当然你可以设置一个默认分类。
- category_map 分类，不明白其作用
- tag_map 标签，不明白其作用

## （6）日期和时间格式配置：

Hexo使用的Moment.js来处理时间的。

- data_format 日期格式，默认为MMM D YYYY，不过我将它改成了YYYY-MM-DD，符合个人口味，其他格式模版可以查看Moment.js
- time_format 时间格式，默认为H:mm:ss

## （7）分页设置：

- per_page 一页显示多少篇文章，0 为不分页，默认值为 10
- pagination_dir 分页目录，默认值为page

## （8）扩展配置：

- theme 主题配置，此处填上主题名就OK了，当然在themes目录下一定要有你配置的主题文件夹。
- deploy 部署配置，将本地public目录也就是网站部署到服务器上的配置。如何部署？Docs文档『基础用法』部分有说明。

参考文献：

[Hexo Docs（一）- 开始准备](http://www.jianshu.com/p/f935e5459c49)