---
title: 使用markdown制作的html幻灯片(1) reveal.js
date: 2017-07-31 20:15:45
tags: 
    - markdown
categories: markdown
---
推荐使用 `reveal.js`
<!-- more -->

# 1. reveal.js 介绍

一个使用 HTML 轻松创建精美的演示文稿框架，你只要有一个支持 CSS 3D 切换的浏览器。
[ demo: http://lab.hakim.se/reveal-js/#/](http://lab.hakim.se/reveal-js/#/)

reveal.js 配备了广泛的功能，包括嵌套幻灯片，Markdown 内容，PDF 导出，演讲笔记和 JavaScript API。还有一个全功能的可视化编辑器和平台：slides.com。

# 2. 使用步骤

- 从  https://github.com/hakimel/reveal.js/ 下载代码

- 进入 reveal.js 文件夹，用浏览器打开 index.html 文件就可以看到效果。

- 修改 index.html 中的 `div class="slides"` 模块为你的内容

# 3. Markdown 语法

## 3.1. data-markdown 属性

   使用 Markdown 实现内容时，需要对 section 标示添加 data-markdown 属性，然后将 Markdown 内容写到一个 text/template 脚本中。
```js
		<div class="reveal">
			<div class="slides">
				<section>Slide 1</section>
				<section data-markdown>
					<script type="text/template">
						## Slide 2
					</script>
				</section>
			</div>
		</div>
```

## 3.2. 分页实现

可以在 section 中通过属性 `data-separator` (水平方向), `data-separator-vertical` (垂直方向) 来划分章节。

For Example:

```js
<section  data-markdown data-separator="---" data-separator-vertical="--"  >
  <script type="text/template">
    # 主题1
    - 主题1-内容1
    - 主题1-内容2
    --
    ## 主题1-内容1
    内容1-细节1
    --
    ## 主题1-内容2
    内容1-细节2
    ---
    # 主题2
  </script>
</section>

```

## 3.3. 外置 Markdown 文件(要求Node.js)

reveal.js 可以引用一个外置的 Markdown 文件来解析。

For Example:
```
<section data-markdown="example.md"
         data-separator="^\n\n\n"
         data-separator-vertical="^\n\n"
         data-separator-notes="^Note:"
         data-charset="iso-8859-15">
</section>

```
data-charset 属性是可选的，它指定加载外部文件时使用的字符集。

当在本地使用，此功能 要求 reveal.js `从本地 Web 服务器中运行`。本地 Web 服务器推荐使用 Node.js。

# 4. 从本地 Web 服务器上运行reveal.js

一些 reveal.js 特征，如外部的 Markdown 和演讲备注，要求演示文稿从本地 Web 服务器上运行。
以下说明将设立这样的服务器，以及所有的进行编辑的 reveal.js 源代码所需的开发服务。

- 下载安装 Node.js https://nodejs.org/zh-cn/

- 克隆 reveal.js 目录 ` git clone https://github.com/hakimel/reveal.js.git`

- 进入 reveal.js 目录导航 `cd reveal.js`

- 安装依赖 `npm install`

- 演示文稿的服务器和监视源文件的修改

- 运行 `$ npm start`,你可以使用 npm start -- --port 8001 修改端口。

- 打开 <http://localhost:8000> 来观看你的演示文稿


参考文献：

[hakimel/reveal.js](https://github.com/hakimel/reveal.js)

[使用markdown制作的html幻灯片有哪些？ - 知乎](https://www.zhihu.com/question/35164931)


[reveal.js（HTML 演示文稿）中文文档](https://vxhly.github.io/2016/09/03/reveal-js-cn-document/)