---
title: “Hexo 系列(7) 百度优化”
tags: 
    - Hexo
    - Hexo优化
categories: Hexo搭建博客
toc: true
abbrlink: 1672863730
date: 2017-07-22 20:15:10
---
百度网站验证
<!-- more -->
# 1. 百度网站验证

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

# 2. 添加 robots.txt 可以不添加

网站通过Robots协议告诉搜索引擎哪些页面可以抓取，哪些页面不能抓取。robots.txt 通常存放于网站根目录。我的 robots.txt 内容为：

```
User-agent: *
Allow: /
Allow: /archives/
Allow: /categories/
Allow: /tags/
Allow: /guestbook/
Allow: /mylove/
Allow: /weblog/
Allow: /page/
Allow: /2016/
Disallow: /vendors/
Disallow: /js/
Disallow: /css/
Disallow: /fonts/
Disallow: /vendors/
Disallow: /fancybox/
Sitemap: http://www.mashangxue123.com/sitemap.xml
```

# 3. 使用各大搜索引擎站长工具

在搜索引擎搜索框输入`site:your.domain` 可以查看域名是否被该搜索引擎收录，用户可以使用各大搜索引擎站长工具提交个人博客网址。

[百度站长平台 http://zhanzhang.baidu.com/linksubmit/url](http://zhanzhang.baidu.com/linksubmit/url)

[360提交入口 http://info.so.360.cn/site_submit.html](http://info.so.360.cn/site_submit.html)

[Google提交入口地址 https://www.google.com/webmasters/tools/home?hl=zh-CN](https://www.google.com/webmasters/tools/home?hl=zh-CN)

# 4. 百度收录

[链接提交_官方课件_站长学院_百度站长平台](http://zhanzhang.baidu.com/college/courseinfo?id=267&page=2#04)

分为四种方式来提交你的链接，

- 主动推送：最为快速的提交方式，推荐您将站点当天新产出链接立即通过此方式推送给百度，以保证新链接可以及时被百度收录。
- 自动推送：最为便捷的提交方式，请将自动推送的JS代码部署在站点的每一个页面源代码中，部署代码的页面在每次被浏览时，链接会被自动推送给百度。可以与主动推送配合使用。
- sitemap：您可以定期将网站链接放到sitemap中，然后将sitemap提交给百度。百度会周期性的抓取检查您提交的sitemap，对其中的链接进行处理，但收录速度慢于主动推送。
- 手工提交：如果您不想通过程序提交，那么可以采用此种方式，手动将链接提交给百度。

## 4.1. 主动推送

### 4.1.1. 在Hexo根目录下 安装插件

```
    npm install hexo-baidu-url-submit --save
```

### 4.1.2. 把以下内容配置到 `_config.yml`文件中

```yml
    baidu_url_submit:
      count: 3 ## 比如3，代表提交最新的三个链接
      host: www.mashangxue123.com ## 在百度站长平台中注册的域名
      token: your_token ## 请注意这是您的秘钥， 请不要发布在公众仓库里!
      path: baidu_urls.txt ## 文本文档的地址， 新链接会保存在此文本文档里
```

### 4.1.3. 查看_config.ym文件中url的值
    必须包含是百度站长平台注册的域名（一般有www）， 比如:

```yml
    # URL
    url: http://www.mashangxue123.com
    root: /
    permalink: :year/:month/:day/:title/

```    

### 4.1.4. 添加一个新的deploy 的类型
 
用减号区分：
```
deploy:
  - type: git
  repo: https://github.com/mashangxue/mashangxue.github.io.git
  branch: master
  - type: baidu_url_submitter
```

执行hexo deploy的时候，新的连接就会被推送了。原理：
- 新链接的产生， hexo generate 会产生一个 `baidu_urls.txt`文本文件，里面包含最新的链接
- 新链接的提交， hexo deploy 会从上述文件中读取链接，提交至百度搜索引擎

## 4.2. 自动推送

如果是next主题，next主题配置文件中的baidu_push设置为true，就可以了。

```bash
# Enable baidu push so that the blog will push the url to baidu automatically which is very helpful for SEO
baidu_push: true
```

## 4.3. 添加并提交sitemap

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

打开http://zhanzhang.baidu.com/linksubmit/url
   点解“网站抓取” “链接提交” 找到 “sitemap”， 把上面的文件加入进去。
   
## 4.4. 向Google提交sitemap文件

 [Google站长工具 https://www.google.com/webmasters/tools](https://www.google.com/webmasters/tools)，
 登录谷歌账号，选择当前站点，左边一栏抓取-站点地图-添加站点地图即可。



[基于Hexo搭建个人博客——进阶篇(从入门到入土)](http://ookamiantd.top/2017/build-blog-hexo-advanced/)
[hexo的next主题个性化教程:打造炫酷网站](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)
[Hexo+nexT主题搭建个人博客](http://www.wuxubj.cn/2016/08/Hexo-nexT-build-personal-blog/)

[github+hexo提交到百度谷歌搜索引擎](http://www.jianshu.com/p/7e1166eb412a)

[hexo干货系列：（六）hexo提交搜索引擎（百度+谷歌）](http://tengj.top/2016/03/14/hexo6seo/)

[Hexo 优化：提交 sitemap 及解决百度爬虫无法抓取 GitHub Pages 链接问题](http://www.yuan-ji.me/Hexo-%E4%BC%98%E5%8C%96%EF%BC%9A%E6%8F%90%E4%BA%A4sitemap%E5%8F%8A%E8%A7%A3%E5%86%B3%E7%99%BE%E5%BA%A6%E7%88%AC%E8%99%AB%E6%8A%93%E5%8F%96-GitHub-Pages-%E9%97%AE%E9%A2%98/)

[Hexo NexT 主题SEO优化指南](https://lancelot_lewis.coding.me/2016/08/16/blog/Hexo-NexT-SEO/)

[动动手指，不限于NexT主题的Hexo优化（SEO篇）](http://www.arao.me/2015/hexo-next-theme-optimize-seo/)

[将hexo博客部署到coding.net](http://www.ieclipse.cn/2016/09/08/Web/hexo-coding-pages/index.html)