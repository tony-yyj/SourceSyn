---
title: main调试带输入参数的程序
tags:
  - C/C++
  - opencv
categories: note
abbrlink: 1014823768
date: 2017-09-10 09:30:00
---

<!-- toc -->
<!-- more -->

# main 函数的 参数 argc,argv 用法

第一个是参数个数，第二个是参数。从2开始计数

当main函数的输入参数为空时，我们可以很方便的通过设置断点，单步运行的方法调试，可是如果需要调试的是有输入参数的程序该怎么办呢？

# VS 设置

英文版：
Project -> Properties -> Configuration Properties -> Debugging
在Command Arguments里填上即可。

中文版：
菜单[项目] -> 属性页 -> 配置属性 -> 调试
在[命令行参数]里填上即可。

记得不同参数之前用空格隔开。如果是地址，记得是//表示路径，因为转义字符的原因

注意：
一定是“[命令行参数] ”  不是第一行的命令那一栏，否则提示找不到文件之类的错误

```bash
C:\\1.jpg C:\\2.jpg C:\\3.jpg
```

# 参考：

* [如何在vs2010中设置C++ main 函数的实参int main（int argc ，char *argv[]）](http://blog.csdn.net/ly763124994/article/details/13627971)

* [Getting Title at 37:11](https://jingyan.baidu.com/article/76a7e409d7ed47fc3b6e15c4.html)

* [C/C++基础知识main函数的参数argc和argv - Eastmount的专栏- CSDN.NET](http://blog.csdn.net/eastmount/article/details/20413773)

* [vs2010下如何调试带输入参数的程序 - thefutureisour的专栏   CSDN.NET](http://blog.csdn.net/thefutureisour/article/details/7686147)

* [main 函数的 参数 argc,argv 用法 - gaoxw0511 - 博客园](http://www.cnblogs.com/xiangwengao/archive/2012/03/30/2425698.html)
