---
title: “Hexo 系列(3) Next 主题配置”
date: 2017-07-20 15:15:04
tags: 博客
categories: 技术
toc: true
---

# hexo-next主题添加近期文章版块

将此代码贴在 `next/layout/_macro/sidebar.swig`中的 `if theme.links` 对应的 `endif` 后面，

```js
{% if theme.recent_posts %}
    <div class="links-of-blogroll motion-element {{ "links-of-blogroll-" + theme.recent_posts_layout  }}">
      <div class="links-of-blogroll-title">
        <!-- modify icon to fire by szw -->
        <i class="fa fa-history fa-{{ theme.recent_posts_icon | lower }}" aria-hidden="true"></i>
        {{ theme.recent_posts_title }}
      </div>
      <ul class="links-of-blogroll-list">
        {% set posts = site.posts.sort('-date') %}
        {% for post in posts.slice('0', '5') %}
          <li>
            <a href="{{ url_for(post.path) }}" title="{{ post.title }}" target="_blank">{{ post.title }}</a>
          </li>
        {% endfor %}
      </ul>
    </div>
{% endif %}
```

主题的_config.yml中添加了几个变量，如下：

recent_posts_title: 近期文章
recent_posts_layout: block
recent_posts: true


# 设置右侧栏头像

编辑站点配置文件，添加如下内容

`avatar: your avatar url`
其中，your avatar url可以是
(1) 完整的互联网URL，你可以先将设置的头像图片放到图床上；
(2) 本地地址：如/upload/image/avatar.png (你需要将avatar.png文件放在/站点目录/source/upload/image/里面)。

# 首页文章以摘要形式显示

最简单的方式是：打开主题配置文件，找到如下位置，修改

```config
auto_excerpt:
  enable: true
  length: 150
```

其中length代表显示摘要的截取字符长度。


# 设置代码高亮主题

NexT 使用 Tomorrow Theme 作为代码高亮，共有5款主题供你选择。 NexT 默认使用的是 白色的 normal 主题，可选的值有 normal，night， night blue， night bright， night eighties：

更改 highlight_theme 字段，将其值设定成你所喜爱的高亮主题，例如：

高亮主题设置示例 `highlight_theme: normal`

# 添加文章末尾版权声明

找到post.swig文件，在footer.post-footer中添加如下代码。

```js
<footer class="post-footer">
    {% if not is_index %}
        <div class="copyright" style="clear:both;">
           <p><span>本文标题:</span><a href="{{ url_for(post.path) }}">{{ post.title }}</a></p>
           <p><span>文章作者:</span><a href="/" title="访问 {{ theme.author }} 的个人博客">{{ theme.author }}</a></p>
           <p><span>发布时间:</span>{{ post.date.format("YYYY年M月D日 - HH时MM分") }}</p>
           <p><span>本文字数:</span><span class="page-count">本文一共有{{ wordcount(page.content) }}字</span></p>
           <p><span>原始链接:</span><a href="{{ url_for(post.path) }}" title="{{ post.title }}">{{ post.permalink }}</a></p>
           <p><span>许可协议:</span><i class="fa fa-creative-commons"></i> <a rel="license" href="http://creativecommons.org/licenses/by-nc/4.0/" title="Attribution-NonCommercial 4.0 International (CC BY-NC 4.0)">Attribution-NonCommercial 4.0</a></p>
           <p><span>转载请保留以上信息。</span></p>
        </div>
      {% endif %}
</footer>
```

然后需要修改一下样式，找到_posts.styl,加入如下样式

```config
.post-footer .copyright{
  padding-top: 1.5em;
  padding-left: 1em;
  font-size: 12px;
  line-height: 1em;
  border:1px solid #ccc;
}
```

# 不蒜子访问统计

搜索关键字busuanzi_count，设置enable: true时，代表开启全局开关。若site_uv、site_pv、page_pv的值均为false时，不蒜子仅作记录而不会在页面上显示。
配置示例如下

```config
busuanzi_count:
  # count values only if the other configs are false
  enable: true
  # custom uv span for the whole site
  site_uv: true
  site_uv_header: 本站访客数
  site_uv_footer: 人次
  # custom pv span for the whole site
  site_pv: true
  site_pv_header: 本站总访问量
  site_pv_footer: 次
  # custom pv span for one page only
  page_pv: true
  page_pv_header: 本文总阅读量
  page_pv_footer: 次

```

# 增加字数统计插件WordCount

这个是看到 一休同学blog 里有这玩意儿，一时好奇也加入了，感觉还挺好玩的，有那么一点简书的味道~

首先在Hexo项目目录下安装：`npm install hexo-wordcount --save`。

在footer.swig文件中加入下面代码

```js
<div class="theme-info">
  <div class="powered-by"></div>
  <span class="post-count">博客全站共{{ totalcount(site) }}字</span>
</div>
```

参考文献：

[++主题配置 - NexT 使用文档](http://theme-next.iissnan.com/theme-settings.html#site-since)

[hexo-next主题添加近期文章版块](http://bigdatadecode.club/hexo-next%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E8%BF%91%E6%9C%9F%E6%96%87%E7%AB%A0%E7%89%88%E5%9D%97.html)

[NexT主题个性化设置](http://www.jeyzhang.com/next-theme-personal-settings.html)

[为 Next 主题文末添加版权等信息](http://ixiusama.com/2016/02/15/%E4%B8%BA%20Next%20%E4%B8%BB%E9%A2%98%E6%96%87%E6%9C%AB%E6%B7%BB%E5%8A%A0%E7%89%88%E6%9D%83%E7%AD%89%E4%BF%A1%E6%81%AF/)