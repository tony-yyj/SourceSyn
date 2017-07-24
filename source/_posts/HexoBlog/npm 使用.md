---
title: “npm 使用”
date: 2017-07-23 15:15:04
tags: 博客
categories: 技术
toc: true
---

# npm常用命令

npm install xxx 安装模块

npm install xxx -g 将模块安装到全局环境中 参考

http://goddyzhao.tumblr.com/post/9835631010/no-direct-command-for-local-installed-command-line-modul

npm ls 查看安装的模块及依赖

npm ls -g 查看全局安装的模块及依赖

npm uninstall xxx  (-g) 卸载模块

npm cache clean 清理缓存.



[安装npm模块 | npm入门](https://chenyiqiao.gitbooks.io/documentation_for_npm/content/install_packages.html)

当你为你的模块安装一个依赖模块时，正常情况下你得先安装他们，在模块根目录下npm install module-name，然后连同版本号手动将他们添加到模块配置文件package.json中的依赖里(dependencies)。

-save和save-dev可以省掉你手动修改package.json文件的步骤。

npm install module-name -save
自动把模块和版本号添加到dependencies部分。

npm install module-name -save-dev
自动把模块和版本号添加到devdependencies部分。

配置文件

package.json提供了三种依赖关系定义：

dependencies
peerDependencies
devDependencies
devDependencies是开发时依赖，比如你模块用了mocha测试框架，那么你的模块的开发就依赖mocha，如果别人想为你的模块贡献代码，他就需要安装mocha。但是只是使用你的模块的人，就不需要mocha。

peerDependencies是为插件准备的。比如grunt的插件，里面没有require(“grunt”)，所以用dependencies会有问题。所以需要单独列出。