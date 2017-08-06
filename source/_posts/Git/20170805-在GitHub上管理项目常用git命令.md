---
title: 在GitHub上管理项目常用git命令
tags:
  - GitHub
  - git
categories: git
abbrlink: 186421960
date: 2017-08-05 17:34:21
---

<!-- toc -->
<!-- more -->

# 1. 在GitHub上新建项目

新建后会有下面的提示：

```bash
…or create a new repository on the command line

echo "# mashangxue1234.github.io" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/mashangxue/mashangxue1234.github.io.git
git push -u origin master

…or push an existing repository from the command line

git remote add origin https://github.com/mashangxue/mashangxue1234.github.io.git
git push -u origin master

 …or import code from another repository 
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.
```

上面对应了三种情形：
第一种从零开始在本地创建一个仓库，添加一个文件，然后提交到github，本文主要讲解这种。
第二种是本地已经有git仓库，只需添加一个远程主机，然后就可以提交本地的内容
第三种是从其它类型的仓库管理工具导入


# 2. 本地新建repository

本地目录下，在命令行里新建一个代码仓库（repository），里面只有一个README.md，命令如下：

## 2.1. 初始化repository

```
　git init
```

## 2.2. 新建一个 README.md文件

可以使用touch命令，或者 echo 命令创建并写入内容，或者自己手动创建
```
　　touch README.md
或者
    echo "# mashangxue123.github.io" >> README.md
```　


## 2.3. 加入到缓存区
```
git add README.md　
```　
（可以用git add --a将所有改动提交到缓存（注意是两个杠））　

## 2.4. 提交改变

并且附上提交信息"first commit"

```
　　git commit -m "first commit"
```

# 3. Push提交到github

## 3.1. 添加远程主机

```
git remote add origin https://github.com/XXX(username)/YYYY(projectname).git
```
加上一个remote的地址，名叫origin，地址是github上的地址（Create a new repo就会有），因为Git是分布式的，所以可以有多个remote.

## 3.2. 推送到远程主机

```
git push origin master
```

## 3.3. 指定一个默认主机

如果当前分支与多个主机存在追踪关系，则可以使用-u选项指定一个默认主机，这样后面就可以不加任何参数使用`git push`

```
git push -u origin master    
```　　
上面命令将本地的master分支推送到origin主机，同时指定origin为默认主机，后面就可以不加任何参数使用 `git push`了

## 3.4. 问题：

此时如果远程仓库origin的master分支上有一些本地没有的提交,push会失败.解决的办法是：

首先设定本地master的上游分支:

```
git branch --set-upstream-to=origin/master
```

然后pull:
```
　　git pull --rebase
```
如果有内容冲突，修改冲突执行
```
   git add .  
   git rebase --continue 
```

最后再push:
```
　　git push
```

如果是新建分支第一次push，会提示：
```
　　fatal: The current branch develop has no upstream branch.
　　To push the current branch and set the remote as upstream, use
　　git push --set-upstream origin develop
```
输入这行命令，然后输入用户名和密码，就push成功了

# 4. 分支

新建好的代码库有且仅有一个主分支（master），它是自动建立的。

## 4.1. 本地新建分支

可以新建分支用于开发：
新建一个叫dev的分支，基于master分支
```
　git branch dev master
```　　
切换到这个分支：
```
　　git checkout dev
```
　　注意：切换分支的时候可以发现，在Windows中的repository文件夹中的文件内容也会实时相应改变，变成当前分支的内容。

## 4.2. 创建分支的另一种方法

```
git checkout -b dev2 develop
```　
可以新建一个分支dev2，同时切换到这个分支

将 dev2 分支删除

```
git branch -d dev2 
```

## 4.3. 分支push到github

比如新建了一个叫dev的分支，而github网站上还没有，可以直接：

```
　　git push -u origin dev
```
## 4.4. 查看分支

`git branch`命令的 `-r` 选项，可以用来查看远程分支， `-a` 选项查看所有分支。

```bash
$ git branch -r
origin/master

$ git branch -a
* master
  remotes/origin/master
```
上面命令表示，本地主机的当前分支是master，远程分支是origin/master。

## 4.5. 删除github上的远程分支

比如github上有 master 和 dev 分支，我现在想着删除 dev 分支，命令如下：

```
git push origin :dev
```
这样就删除了，下面是删除成功提示
```
To https://github.com/mashangxue/mashangxue123.git
 - [deleted]         dev
```

## 4.6. 将Develop分支发布到Master分支

```bash
　　# 切换到Master分支
　　git checkout master

　　# 对Develop分支进行合并
　　git merge --no-ff develop

```
--no-ff参数意义：
默认情况下，Git执行"快进式合并"（fast-farward merge），会直接将Master分支指向Develop分支。
使用--no-ff参数后，会执行正常合并，在Master分支上生成一个新节点。日志看起来好看，版本演进的清晰。
merge的时候如果遇到冲突，就手动解决，然后重新add，commit即可。

# 5. 参考文献

[Git查看、删除、重命名远程分支和tag](https://blog.zengrong.net/post/1746.html)

[Git - 分支的新建与合并](https://git-scm.com/book/zh/v1/Git-%E5%88%86%E6%94%AF-%E5%88%86%E6%94%AF%E7%9A%84%E6%96%B0%E5%BB%BA%E4%B8%8E%E5%90%88%E5%B9%B6)

[Git远程操作详解 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2014/06/git_remote.html)

[Git分支管理策略 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2012/07/git.html)

[++ 在GitHub上管理项目 - 圣骑士wind - 博客园](http://www.cnblogs.com/mengdd/p/3447464.html)