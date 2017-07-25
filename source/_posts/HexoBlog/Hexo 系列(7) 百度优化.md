---
title: “Hexo 系列(7) 百度优化”
date: 2017-07-22 20:15:10
tags: 博客
categories: 技术
toc: true
---
百度网站验证
<!-- more -->
# 百度网站验证

百度提交入口
[链接提交_站长工具_优化PC和移动搜索收录_百度站长平台](http://zhanzhang.baidu.com/linksubmit/url)

打开百度站长验证网站
方式一：文件验证

- 登录百度站长选择添加网站，使用方式为文件验证
- 将下载的文件放到 `source`文件下
- 由于hexo自动会对html文件进行渲染，所以在站点配置文件中找到 `skip_render`:
  在后面添加文件名字，如有多个用[a.html,b.html]，eg:skip_render:[baidu_verify_tdOGHi8IQG.html, baidu_verify_vcJkI72f1e.html]
- 重新渲染文件

```
hexo clean
hexo d -g
```

然后可以点击百度站长的验证按钮了

 如果还是 不成功，就直接把 百度下载的这个文件拷贝到deploy_git目录下面覆盖Hexo自己生成的那个文件。我的就是这样搞定。

方式二：CNAME验证

- 去站长添加网站选择CNAME验证
- 把地址解析到zz.baidu.com
- 完成验证

# 添加并提交sitemap

安装hexo的sitemap网站地图生成插件:

```
npm install hexo-generator-sitemap --save
npm install hexo-generator-baidu-sitemap --save
```
在站点配置文件中添加如下代码。


```
# hexo sitemap
sitemap:
  path: sitemap.xml
baidusitemap:
  path: baidusitemap.xml
```

配置成功后，会生成sitemap.xml和baidusitemap.xml，前者适合提交给谷歌搜素引擎，后者适合提交百度搜索引擎


[基于Hexo搭建个人博客——进阶篇(从入门到入土)](http://ookamiantd.top/2017/build-blog-hexo-advanced/)
[hexo的next主题个性化教程:打造炫酷网站](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)