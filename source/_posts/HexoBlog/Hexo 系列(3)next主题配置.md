---
title: “Hexo 系列(3) Next 主题配置”
tags: 
    - Hexo
    - Hexo优化
    - Next主题
categories: Hexo搭建博客
toc: true
abbrlink: 3927767946
date: 2017-07-20 19:17:07
---
Hexo 的next主题配置优化，新增各种功能功能包括：添加近期文章版块、设置右侧栏头像、首页文章以摘要形式显示、代码高亮主题、添加文章末尾版权声明、不蒜子访问统计、增加字数统计、录默认全展开、百度统计等
<!-- more -->
# 1. hexo-next主题添加近期文章版块

将下面的代码贴在 `next/layout/_macro/sidebar.swig`中的 `if theme.links` 对应的 `endif` 后面，

```javascript
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


# 2. 设置右侧栏头像

编辑站点配置文件 `_config.yml`，添加如下内容

`avatar: XX.jpg`

其中，XX.jpg可以是：

(1) 完整的互联网URL，你可以先将设置的头像图片放到图床上；

(2) 站点内的地址，例如：

- /uploads/mashangxue123.jpg 需要将你的头像图片放置在 站点的 source/uploads/（可能需要新建uploads目录）
- `avatar: /images/mashangxue123.jpg` 需要将你的头像图片放置在 主题的 source/images/ 目录下。


# 3. 首页文章以摘要形式显示

方法1：打开主题配置文件，找到如下位置，修改

```config
auto_excerpt:
  enable: true
  length: 150
```

其中length代表显示摘要的截取字符长度。

方法2：

在文章中使用 `<!-- more -->` 手动进行截断，这是Hexo 提供的方式.
推荐使用 这种，除了可以精确控制需要显示的摘录内容以外， 这种方式也可以让 Hexo 中的插件更好的识别。

方法3：
在文章的 front-matter 中添加 `description`，并提供文章摘录

# 4. 设置代码高亮主题

NexT 使用 Tomorrow Theme 作为代码高亮，共有5款主题供你选择。 NexT 默认使用的是 白色的 normal 主题，可选的值有 `normal，night， night blue， night bright， night eighties`：

更改 highlight_theme 字段，将其值设定成你所喜爱的高亮主题，例如： `highlight_theme: normal`

# 5. 添加文章末尾版权声明

打开下面的配置即可：

```config
# Declare license on posts
post_copyright:
  enable: true
  license: CC BY-NC-SA 3.0
  license_url: https://creativecommons.org/licenses/by-nc-sa/3.0/
```

或者自定义如下：

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

# 6. 不蒜子访问统计

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

# 7. 增加字数统计插件WordCount

首先在Hexo项目目录下安装：`npm install hexo-wordcount --save`。

在footer.swig文件中加入下面代码

```
<div class="theme-info">
  <div class="powered-by"></div>
  <span class="post-count">博客全站共{{ totalcount(site) }}字</span>
</div>

```

# 8. 目录默认全展开

在 `~/themes/next/source/css/_custom/custom.styl` 中添加以下代码：

```
.post-toc .nav .nav-child { display: block; }
```

# 9. 去掉Hexo博客底部页脚

只需要配置一下就可以：

```
# Footer `powered-by` and `theme-info` copyright
copyright: false
```

相关的代码在footer.swig中的带有powered-by 的div标签

# 10. 百度统计

登录 `百度统计`，定位到站点的代码获取页面
复制 hm.js? 后面那串统计脚本 id

# 11. 侧边栏推荐阅读

打开主题配置文件修改(links里面写你想要的推荐链接):

```yml
# Blogrolls
links_title: 推荐阅读
#links_layout: block
links_layout: inline
links:
  百度前端技术学院: http://ife.baidu.com/

```

# 12. 在右上角或者左上角实现fork me on github

点击[https://github.com/blog/273-github-ribbons](https://github.com/blog/273-github-ribbons) 挑选自己喜欢的样式，并复制代码。
例如我的代码是：
```
<a href="https://github.com/mashangxue"><img style="position: absolute; top: 0; left: 0; border: 0;" src="https://camo.githubusercontent.com/82b228a3648bf44fc1163ef44c62fcc60081495e/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f6769746875622f726962626f6e732f666f726b6d655f6c6566745f7265645f6161303030302e706e67" alt="Fork me on GitHub" data-canonical-src="https://s3.amazonaws.com/github/ribbons/forkme_left_red_aa0000.png"></a>
```
然后粘贴刚才复制的代码到 `themes/next/layout/_layout.swig`文件中(放在<div class="headband"></div>的下面)，
并把href改为你的github地址.

# 13. 添加 LiveRe 评论支持

进入 https://livere.com/，注册账号, 生成代码，data-uid 即为所需 uid

站点配置文件中设置： `livere_uid: your uid`

[hexo从多说评论转为韩国来必力评论](https://zengmianhui.github.io/2017/05/02/hexo%E4%BB%8E%E5%A4%9A%E8%AF%B4%E8%AF%84%E8%AE%BA%E8%BD%AC%E4%B8%BA%E9%9F%A9%E5%9B%BD%E6%9D%A5%E5%BF%85%E5%8A%9B%E8%AF%84%E8%AE%BA/)

# 14. 集成百度分享

编辑 站点配置文件中

```yml
baidushare: 
  type: button #百度分享展示的方式button|slide

```

# 15. 关键词keywords

默认next主题的文章关键字取文章的标签，所以如果想要设置很全的关键字，肯定会造成自己的标签页的标签过多，看着过于杂乱.

- 文章的头部新增 keywords 字段，新建文章的时候设置。
- 在next主题的配置_config.yml文件，设置主题的keywords。

涉及代码/themes/layout/_partial/Head.swg中,
从代码可以看出，优先使用page中的关键字keywords，然后是page中的tags，最后是主题中的关键字。

```swig
{% if page.keywords %}
  <meta name="keywords" content="{{ page.keywords }}" />
{% elif page.tags and page.tags.length %}
  <meta name="keywords" content="{% for tag in page.tags %}{{ tag.name }},{% endfor %}" />
{% elif theme.keywords %}
  <meta name="keywords" content="{{ theme.keywords }}" />
{% endif %}
```


# 16. 参考文献：

[++主题配置 - NexT 使用文档](http://theme-next.iissnan.com/theme-settings.html#site-since)

[hexo-next主题添加近期文章版块](http://bigdatadecode.club/hexo-next%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E8%BF%91%E6%9C%9F%E6%96%87%E7%AB%A0%E7%89%88%E5%9D%97.html)

[NexT主题个性化设置](http://www.jeyzhang.com/next-theme-personal-settings.html)

[为 Next 主题文末添加版权等信息](http://ixiusama.com/2016/02/15/%E4%B8%BA%20Next%20%E4%B8%BB%E9%A2%98%E6%96%87%E6%9C%AB%E6%B7%BB%E5%8A%A0%E7%89%88%E6%9D%83%E7%AD%89%E4%BF%A1%E6%81%AF/)

[使用 Hexo 搭建博客的深度优化与定制](http://blog.tangxiaozhu.com/p/45374067/)

[Hexo+nexT主题搭建个人博客](http://www.wuxubj.cn/2016/08/Hexo-nexT-build-personal-blog/)

[Hexo优化（5）：添加网站访问统计](https://crane-yuan.github.io/2016/03/25/Hexo-05-add-site-statistics/)

[第三方服务集成 - NexT 使用文档](http://theme-next.iissnan.com/third-party-services.html#analytics-baidu)

[打造个性超赞博客Hexo+NexT+GithubPages的超深度优化](https://reuixiy.github.io/technology/computer/computer-aided-art/2017/06/09/hexo-next-optimization.html)

[hexo的next主题个性化教程:打造炫酷网站](http://shenzekun.cn/hexo%E7%9A%84next%E4%B8%BB%E9%A2%98%E4%B8%AA%E6%80%A7%E5%8C%96%E9%85%8D%E7%BD%AE%E6%95%99%E7%A8%8B.html)

[基于Hexo搭建个人博客——进阶篇(从入门到入土)](http://ookamiantd.top/2017/build-blog-hexo-advanced/)

[为NexT主题添加文章阅读量统计功能](https://notes.wanghao.work/2015-10-21-%E4%B8%BANexT%E4%B8%BB%E9%A2%98%E6%B7%BB%E5%8A%A0%E6%96%87%E7%AB%A0%E9%98%85%E8%AF%BB%E9%87%8F%E7%BB%9F%E8%AE%A1%E5%8A%9F%E8%83%BD.html)