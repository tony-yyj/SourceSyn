---
title: “Hexo 系列(7) 报错总结”
date: 2017-07-23 15:15:04
tags: 博客
categories: 技术
toc: true
---
# npm install hexo --no-optional不好使

更换npm淘宝镜像https://npm.taobao.org/

# ERROR Deployer not found: git 或者 ERROR Deployer not found: github

解决方法： npm install hexo-deployer-git --save

如发生报错： `ERROR Process failed: layout/.DS_Store` , 那么进入主题里面layout和_partial目录下，使用删除命令：

`rm -rf .DS_Store`

# ERROR Plugin load failed: hexo-server

原因：

Besides,utilities are separated into a standalone module.hexo.util is not reachable anymore.

解决方法，执行命令：

`sudo npm install hexo-server`

# 执行命令hexo server，提示：Usage: hexo ....

原因：没有生成本地服务

解决方法，执行命令：

`npm install hexo-server --save`

