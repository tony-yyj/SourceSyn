---
title: Hexo 增加阅读次数
abbrlink: 2160352618
date: 2017-07-26 21:23:57
tags: 
    - Hexo
    - Hexo优化
    - Next主题
categories: Hexo搭建博客
---

<!-- more -->

# 注册leancloud帐号
  https://leancloud.cn/
  
# 创建Lean Cloud应用

体步骤如下：

- 首先到『控制台』创建一个应用，名字随便取。
- 点击新建应用的『数据』选项，选择『创建Class』，取名为”Counter“。
- 点击新建应用右上角的齿轮,设置，在『应用Key』选项里得到APP ID 和 APP Key，在后面会用到。
- 回到设置中，选择安全中心，在Web安全域名中添加博客地址

# 设置主题配置文件

_config.yml中的leancloud_visitors字段enable: true，实现阅读数量的统计

```
leancloud_visitors:
  enable: true
  app_id: #你的app_id
  app_key: #你的的app_key
```

# 部署后才能显示

[Hexo统计post阅读次数 ](http://www.icafebolger.com/hexo/hexopostcount.html)

[使用LeanCloud平台为Hexo博客添加文章浏览量统计组件](http://crescentmoon.info/2014/12/11/popular-widget/)

[Hexo搭建博客教程 增加阅读排行统计页面](https://thief.one/2017/03/03/Hexo%E6%90%AD%E5%BB%BA%E5%8D%9A%E5%AE%A2%E6%95%99%E7%A8%8B/)

[使用leancloud给博客添加阅读次数](https://qinzhaokun.github.io/2017/06/10/%E4%BD%BF%E7%94%A8leancloud%E7%BB%99%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0%E9%98%85%E8%AF%BB%E6%AC%A1%E6%95%B0/)

[nMask&#39;s 排行榜效果 Blog](https://thief.one/count/)

[++Hexo的NexT主题个性化：添加文章阅读量](http://www.jeyzhang.com/hexo-next-add-post-views.html)