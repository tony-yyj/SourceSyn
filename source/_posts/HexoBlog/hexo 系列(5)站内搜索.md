---
title: “Hexo 系列(5) 站内搜索”
date: 2017-07-20 19:25:09
tags: 博客
categories: 技术
toc: true
---
主要是 Local Search，Algolia 最新版本一直配置失败， Swiftype需要企业邮箱
<!-- more -->
# 1. 使用Local Search

## 1.1. 安装 hexo-generator-searchdb，

## 1.2. 在站点的根目录下执行以下命令：

  `npm install hexo-generator-searchdb --save`

## 1.3. 编辑 `站点配置`文件，新增以下内容到任意位置：

```
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

## 1.4. 编辑 `主题配置`文件，启用本地搜索功能：

```
# Local search
local_search:
  enable: true
```

## 1.5. Algolia 最新版本一直配置失败

## 1.6. Swiftype需要企业邮箱

# 2. 参考文献

[hexo干货系列：（五）hexo添加站内搜索 用swiftype ](http://tengj.github.io/2016/03/11/hexo5Swiftype/)

[配置algolia，跟新algolia失败 ·apiKey  提示找不到 Issue #1293 · iissnan/hexo-theme-next](https://github.com/iissnan/hexo-theme-next/issues/1293)

[利用swiftype为hexo添加站内搜索v2.0 | JerryFu&#39;s Blog](http://www.jerryfu.net/post/search-engine-for-hexo-with-swiftype-v2.html)

[个人搭建hexo并部署到github期间遇到的问题](http://lijialalala.github.io/2016/04/05/hexoxo-usage/)

[+++第三方服务集成 - NexT 使用文档](http://theme-next.iissnan.com/third-party-services.html#search-system)

[hexo干货系列：（六）hexo提交搜索引擎（百度+谷歌）](http://tengj.github.io/2016/03/14/hexo6seo/)

