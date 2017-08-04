---
title: Hexo 多台电脑同步 源码保存
abbrlink: 3611120980
date: 2017-07-25 17:42:19
tags: 
    - Hexo
    - Hexo优化
categories: Hexo
alias: 3611120980/
---
多台电脑同步博客源码，首先要把最新的源码上传到git上，然后在其它电脑上搭建Hexo环境后同步博客源码。 前提是两台电脑都能连上git，主要是都配置了 `git ssh`密钥连接
<!-- more -->

# 1. 同步博客源码到git

在你打算上传的最新博客源码上按照下面操作

## 1.1. 编辑.gitignore文件：

`.gitignore`文件作用是声明不被git记录的文件，blog根目录下的 `.gitignore`是hexo初始化是创建的，可以直接编辑，建议.gitignore文件包括以下内容：

```gitignore
.DS_Store      
Thumbs.db      
db.json      
*.log      
node_modules/      
public/      
.deploy*/
```

说明：
public内的文件可以根据source文件夹内容自动生成的，不需要备份。其他日志log、压缩、数据库Thumbs.db等文件也都是调试等使用，也不需要备份。

## 1.2. 初始化仓库

```bash
git init    
git remote add origin https://github.com/mashangxue/SourceSyn.git # 将本地仓库映射到托管服务器的仓库
```

server是仓库的在线目录地址，可以从git上直接复制过来，origin是本地分支，remote add会将本地仓库映射到托管服务器的仓库上。

## 1.3. 添加本地文件到仓库并同步到git上

```bash
git add . #添加blog目录下所有文件，注意有个'.'(.gitignore里面声明的文件不在此内)    
git commit -m "hexo source first add" #添加更新说明    
git push -u origin master  #推送更新到git上

```

# 2. 将git的内容同步到另一台电脑

假设已经将blog源码内容备份到了git上，现在准备在新电脑上同步源码内容。

## 2.1. 先建好hexo的环境

```bash
npm install -g hexo-cli  # 安装hexo
 
hexo init myblog         #用hexo创建一个博客目录
cd myblog
npm install

npm install hexo-deployer-git --save # 部署安装 hexo-deployer-git
```

## 2.2. 拉取源代码

在建好的环境的主目录运行以下命令

```bash
git init       #将目录添加到版本控制系统中    
git remote add origin https://github.com/mashangxue/SourceSyn.git #将本地仓库映射到托管服务器的仓库上    
git fetch --all  #将git上所有文件拉取到本地    
git reset --hard origin/master  #强制将本地内容指向刚刚同步git云端内容,用远端文件覆盖本地相同文件
```

reset对所拉取的文件不做任何处理，此处不用pull是因为本地尚有许多文件，使用pull会有一些版本冲突，解决起来也麻烦，而本地的文件都是初始化生成的文件，较拉取的库里面的文件而言基本无用，所以直接丢弃。

## 2.3. 更新文章到git

要将新电脑上的最新的文章更新到git。在本地文件中运行以下命令：

```bash
git status #查看本地文件的状态。
git add . #将所有更新的本地文件添加到版本控制系统中

git commit -m '更新信息说明' 
git push
```

# 3. 同步文章

只需运行：

```bash
git pull
```

获取的源码即为最新文件

参考文献：

[基于Hexo搭建个人博客——进阶篇(从入门到入土) 多PC同步源码篇 ](http://ookamiantd.top/2017/build-blog-hexo-advanced/)