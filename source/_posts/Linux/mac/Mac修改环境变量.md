---
title: Mac系统设置环境变量
tags:
  - Linux
  - Mac
categories: Mac
date: 2017-09-08 19:00:00
---
命令：`vi ~/.bash_profile` 添加  `export PATH=$PATH:yourpath1`
<!-- toc -->
<!-- more -->

# 1. OS X系统环境变量,加载顺序为：

* /etc/profile
* /etc/paths
* ~/.bash_profile , ~/.bash_login ,  ~/.profile 按照从前往后的顺序读取,只会读取一个
* ~/.bashrc

## 1.1. `/etc/profile和/etc/paths`是系统级别的

系统启动就会加载,后面几个是当前用户级的环境变量。

## 1.2. `~/.bash_profile，~/.bash_login，~/.profile`按照从前往后的顺序读取

如果~/.bash_profile文件存在，则后面的几个文件就会被忽略不读了，
如果~/.bash_profile文件不存在，才会以此类推读取后面的文件。
/etc/profile对所有用户生效，~/.bash_profile只对当前用户生效。

## 1.3. ~/.bashrc没有上述规则，它是bash shell打开的时候载入的。

如果默认shell是bash，那么shell启动时会触发.bashrc，如果默认shell是zsh，那么shell启动时会触发.zshrc
**一般我们修改这个文件`~/.bashrc`可以了**

# 2. PATH的语法为如下

```bash
# 语法，中间用冒号隔开
export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N>
# 举例
export PATH=$PATH:/opt/local/bin:/opt/local/sbin
```

配置立即生效，否则就关闭终端重新打开

```
source ~/.bash_profile
```

查看是否生效
```
echo $PATH
```

# 3. 详细设置环境变量

## 3.1. 全局设置

## 3.2. 方法一`/etc/paths`：

```
sudo vi /etc/paths
```
编辑 paths，将环境变量添加到 paths 中。
小技巧：输入环境变量时，不用一个一个地输入，只要拖动文件夹到 Terminal 里就可以了。

## 3.3. 方法二`/etc/paths.d/name`：

好处：自己生成新的文件，不用把变量全都放到 paths 一个文件里，方便管理。

用touch创建一个文件：

```
sudo touch /etc/paths.d/mysql
```

用 vim 打开这个文件：

```
sudo vim /etc/paths.d/mysql
```

编辑该文件，键入路径并保存

```
/usr/local/mysql/bin
```

用source命令直接激活，或者关闭该 Terminal 窗口并重新打开一个，就能使用 mysql 命令了

## 3.4. 单个用户设置

打开 用户目录

注意： **Mac 是 .bash_profile 而Linux 里面是 .bashrc**

```bash
cd ~
# Linux 里面是 .bashrc, mac可以使用 open -e .bash_profile 弹出可视化编辑窗口
vim ~/.bash_profile

# 把下面命令添加到上面的文件
export PATH="/Users/mashangxue/anaconda3/bin:$PATH"

# 查看PATH
echo $PATH
```

[Mac添加环境变量全面解读 ](http://blog.csdn.net/jackuhan/article/details/51868395)
[MAC 设置环境变量PATH 和 查看PATH](http://www.jianshu.com/p/acb1f062a925)