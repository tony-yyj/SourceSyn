---
title: 如何在markdown中插入数学公式
tags:
  - markdown
categories: markdown
date: 2017-09-08 21:00:00
---
<!-- toc -->
<!-- more -->

# 1. VS code编辑器直接安装插件
mdmath允许使用Visual Studio代码作为可以排版和渲染TeX数学的markdown编辑器。

[https://github.com/goessner/mdmath](https://github.com/goessner/mdmath)

Windows安装方法，运行下面的命令
```
cd  %USERPROFILE%\.vscode\extensions
git clone https://github.com/goessner/mdmath.git
cd mdmath
npm install
```

Mac & Linux Command Line

```
cd $HOME/.vscode/extensions
git clone https://github.com/goessner/mdmath.git
cd mdmath
npm install
```

# 2. 使用MathJax引擎

MathJax 是一个显示网络上数学公式的JS引擎，使用MathJax引擎仅需要引入：
```
<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
```

行间公式： $$公式$$
```
$$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$
```
行内公式：\[公式\]表示行间公式。因为Markdown中\是转义字符

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>
\\(x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}\\)

# 3. 测试公式

$$E = mc^2$$

$$
x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$

行内公式$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$

$$
\begin{array}{c|lcr}
n & \text{Left} & \text{Center} & \text{Right} \\
1 & 0.24 & 1 & 125 \\
2 & -1 & 189 & -8 \\
3 & -20 & 2000 & 1+10i \\
\end{array}
$$

$$
        \begin{matrix}
        1 & x & x^2 \\
        1 & y & y^2 \\
        1 & z & z^2 \\
        \end{matrix}
$$

# 4. GitHub 录入数学公式

CodeCogs 提供了一个在线 LaTeX 编辑器 https://www.codecogs.com/latex/eqneditor.php

可以将输入的数学公式转换为图片，并自动生成 HTML 代码(网站底部有代码),直接把生成的代码粘贴过去就可以了

<a href="https://www.codecogs.com/eqnedit.php?latex=ax^{2}&space;&plus;&space;by^{2}&space;&plus;&space;c&space;=&space;0" target="_blank"><img src="https://latex.codecogs.com/png.latex?ax^{2}&space;&plus;&space;by^{2}&space;&plus;&space;c&space;=&space;0" title="ax^{2} + by^{2} + c = 0" /></a>

<img src="https://latex.codecogs.com/png.latex?\bg_white&space;ax^{2}&space;&plus;&space;by^{2}&space;&plus;&space;c&space;=&space;0" title="ax^{2} + by^{2} + c = 0" />

```
<img src="https://latex.codecogs.com/png.latex?ax^{2}&space;&plus;&space;by^{2}&space;&plus;&space;c&space;=&space;0" title="ax^{2} + by^{2} + c = 0" />
```

# 5. 使用Google Chart的服务器

```
<img src="http://chart.googleapis.com/chart?cht=tx&chl= 在此插入Latex公式" style="border:none;">
```
示例如下：

```
<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" style="border:none;">
```

公式显示结果为：

<img src="http://chart.googleapis.com/chart?cht=tx&chl=\Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}" style="border:none;">

适用了下，Google Chart服务器的响应速度还可以

# 6. 使用forkosh服务器

forkosh上提供了关于Latex公式的一份简短而很有用的帮助，参考[http://www.forkosh.com/mathtextutorial.html]

使用forkosh插入公式的方法是

```
<img src="http://www.forkosh.com/mathtex.cgi? 在此处插入Latex公式">
```

示例如下：

```
<img src="http://www.forkosh.com/mathtex.cgi? \Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}">
```

<img src="http://www.forkosh.com/mathtex.cgi? \Large x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}">
<img src="/cgi-bin/mathtex.cgi?\sqrt{a^2+b^2}">

# 7. 参考文献：

* [如何在markdown中插入数学公式](http://www.jianshu.com/p/888c5eaebabd).

* [在线编辑工具Online LaTeX Equation Editor - create, integrate and download](http://www.codecogs.com/latex/eqneditor.php)

* [Markdown中插入数学公式的方法](http://zyy1217.com/2016/08/01/Markdown%E4%B8%AD%E6%8F%92%E5%85%A5%E6%95%B0%E5%AD%A6%E5%85%AC%E5%BC%8F%E7%9A%84%E6%96%B9%E6%B3%95/)

* [++Mathjax与LaTex公式简介 | Ryan Zhao](http://mlworks.cn/posts/introduction-to-mathjax-and-latex-expression/)

* [MathJax](https://www.mathjax.org/)

* [在markdown里如何写数学公式](http://magicly.me/2017/03/02/markdown-math/)

* [在线 LaTeX 公式编辑器](https://www.codecogs.com/latex/eqneditor.php?lang=zh-cn)

* [+++在线公式代码编辑器Math](https://webdemo.myscript.com/views/math.html#)

* [数学符号查询Detexify LaTeX handwritten symbol recognition](http://detexify.kirelabs.org/classify.html)

* [MathJax-在网页或MarkDown中插入数学公式](http://weilai5432.github.io/2017/01/11/MathJax-%E5%9C%A8MarkDown%E4%B8%AD%E6%8F%92%E5%85%A5%E6%95%B0%E5%AD%A6%E5%85%AC%E5%BC%8F/)

* [Your Paper -  Overleaf](https://www.overleaf.com/10209622bsrnnvzvjfzk#/37763937/)

* [ mathtex.html ](http://www.forkosh.com/mathtex.html)

* [一份其实很短的 LaTeX 入门文档](https://liam0205.me/2014/09/08/latex-introduction/)