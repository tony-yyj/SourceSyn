---
title: “npm 使用”
tags: 
    - npm
    - Hexo
categories: 
    - 前端
toc: true
abbrlink: 3473012492
date: 2017-07-23 18:15:11
alias: 3473012492/
---
淘宝 NPM 镜像配置，基本命令使用
<!-- more -->
# 淘宝 NPM 镜像
https://npm.taobao.org/
[淘宝 NPM 镜像](https://npm.taobao.org/)

使用说明:

你可以使用定制的 cnpm 命令行工具代替默认的 npm:

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

或者你直接通过添加 npm 参数 alias 一个新命令:

```bash
alias cnpm="npm --registry=https://registry.npm.taobao.org \
--cache=$HOME/.npm/.cache/cnpm \
--disturl=https://npm.taobao.org/dist \
--userconfig=$HOME/.cnpmrc"

# Or alias it in .bashrc or .zshrc

$ echo '\n#alias for cnpm\nalias cnpm="npm --registry=https://registry.npm.taobao.org \
  --cache=$HOME/.npm/.cache/cnpm \
  --disturl=https://npm.taobao.org/dist \
  --userconfig=$HOME/.cnpmrc"' >> ~/.zshrc && source ~/.zshrc

```

# npm常用命令

运行 `npm -v`出现版本提示表示安装成功:

升级 `npm install npm -g`

npm install xxx 安装模块

npm install xxx -g 将模块安装到全局环境中

npm ls 查看安装的模块及依赖

npm ls -g 查看全局安装的模块及依赖

npm uninstall xxx  (-g) 卸载模块

npm cache clean 清理缓存.


[http://www.runoob.com/nodejs/nodejs-npm.html](http://www.runoob.com/nodejs/nodejs-npm.html)

[安装npm模块 | npm入门](https://chenyiqiao.gitbooks.io/documentation_for_npm/content/install_packages.html)

# -save和save-dev

当你为你的模块安装一个依赖模块时，正常情况下你得先安装他们，在模块根目录下npm install module-name，然后连同版本号手动将他们添加到模块配置文件package.json中的依赖里(dependencies)。

-save和save-dev可以省掉你手动修改package.json文件的步骤。

```
npm install module-name -save

```
自动把模块和版本号添加到dependencies部分。

```
npm install module-name -save-dev

```
自动把模块和版本号添加到devdependencies部分。

package.json 位于模块的目录下，用于定义包的属性。接下来让我们来看下 express 包的 package.json 文件，位于 node_modules/express/package.json 内容