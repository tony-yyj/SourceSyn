---
title: Hexo使用mathjax输入数学公式
tags: 
    - Hexo 
    - mathjax
categories: Hexo
abbrlink: 1521650214
abbrlinkurl: '原文 http://www.mashangxue123.com/undefined/1521650214'
date: 2017-08-03 14:56:50
mathjax: ture
---

<!-- toc -->
<!-- more -->

# 1. NexT如何集成 mathjax

可以在主题的 _config.xml 配置打开即可，因为Next自带了对数学公式的支持，

把 mathjax 使能为true， cdn 设置为 `//cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML`
per_page代表是否不渲染每一页，我们设置为true，表示只有在有mathjax 头标签的时候才渲染公式。（这个可以从源代码mathjax.swig 文件中看出来）
```
{% if theme.mathjax.enable %}
  {% if not theme.mathjax.per_page or (page.total or page.mathjax) %}
```

# 2. 框架不提供怎么集成mathjax

只需要集成的页面上加载一个script即可：

```js
<script type="text/javascript"
   src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>

```

也可以再加入math样式相关代码
```js
<script type="text/x-mathjax-config">
    MathJax.Hub.Config({"HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX","TeX"], linebreaks: { automatic:true }, EqnChunk: (MathJax.Hub.Browser.isMobile ? 10 : 50) },
        tex2jax: { inlineMath: [ ["$", "$"], ["\\(","\\)"] ], processEscapes: true, ignoreClass: "tex2jax_ignore|dno",skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code']},
        TeX: {  noUndefined: { attributes: { mathcolor: "red", mathbackground: "#FFEEEE", mathsize: "90%" } }, Macros: { href: "{}" } },
        messageStyle: "none"
    }); 
</script>

<script type="text/x-mathjax-config">
    MathJax.Hub.Queue(function() {
        var all = MathJax.Hub.getAllJax(), i;
        for(i=0; i < all.length; i += 1) {
            all[i].SourceElement().parentNode.className += ' has-jax';
        }
    });
</script>

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML">
</script>
```

# 3. 安装插件

## 3.1. 安装命令
```
npm install hexo-math --save
```
https://github.com/hexojs/hexo-math 

## 3.2. 配置站点
下面内容是在站点配置设置，我的设置后出错。 最终只是需要安装就可以正常运行，不需要下面的配置。

```yml
math:
  engine: 'mathjax' # or 'katex'
  mathjax:
    src: custom_mathjax_source
    config:
      # MathJax config
  katex:
    css: custom_css_source
    js: custom_js_source # not used
    config:
      # KaTeX config
```


# 4. 测试例子

## 4.1. 一行代码

```
 一行代码 $a = b + c$
```
 $a = b + c$

## 4.2. 多行代码

```
$$\frac{\partial u}{\partial t}
= h^2 \left( \frac{\partial^2 u}{\partial x^2} +
\frac{\partial^2 u}{\partial y^2} +
\frac{\partial^2 u}{\partial z^2}\right)$$

```

$$\frac{\partial u}{\partial t}
= h^2 \left( \frac{\partial^2 u}{\partial x^2} +
\frac{\partial^2 u}{\partial y^2} +
\frac{\partial^2 u}{\partial z^2}\right)$$

## 4.3. 使用Tag的块, 需要按照math插件

```
{% math %}
\begin{aligned}
\dot{x} & = \sigma(y-x) \\
\dot{y} & = \rho x - y - xz \\
\dot{z} & = -\beta z + xy
\end{aligned}
{% endmath %}

```

# 5. LaTex 公式渲染与 Markdown 渲染冲突问题

在markdown中使用mathjax下标_时，记得一定要写成\_，否则将会出现不能解析的情况。

Markdown 解析和 LaTex 公式解析时出现冲突，典型情况就是：如果希望 LaTex 公式中的下划线 _ 解析成功，必须写成 \_ 强制转义。这是说，如下的公式：

```
$F_a = F_b + F_c + F_{\mu}$
```

$F_a = F_b + F_c + F_{\mu}$

不会被渲染，必须修改为：

```
$F\_a = F\_b + F\_c + F\_{\mu}$
```

$F\_a = F\_b + F\_c + F\_{\mu}$

也可以使用标签的方式不用大规模改动 LaTex 公式

```
 {% math %} F_a = F_b + F_c + F_{\mu} {% endmath %}
```

参考文献

[++ 在 Hexo 中完美使用 Mathjax 输出数学公式](http://lukang.me/2014/mathjax-for-hexo.html)

Mathjax官方文档， http://docs.mathjax.org/en/latest/start.html 
 [Getting Started &mdash; MathJax 2.7 documentation](http://docs.mathjax.org/en/latest/start.html)


[在线识别手写数学公式的工具 Math](https://webdemo.myscript.com/views/math.html#)

[Hexo-NexT主题使用mathjax输入数学公式注意事项](http://www.befuncool.com/2016/11/20/Hexo-NexT%E4%B8%BB%E9%A2%98%E4%BD%BF%E7%94%A8mathjax%E8%BE%93%E5%85%A5%E6%95%B0%E5%AD%A6%E5%85%AC%E5%BC%8F%E6%B3%A8%E6%84%8F%E4%BA%8B%E9%A1%B9/)