---
title: Linux设置环境变量
tags:
  - Linux
categories: Linux
abbrlink: 2613038403
date: 2017-09-08 20:00:00
---
命令：`vi ~/.bash_profile` 添加  `export PATH=$PATH:yourpath1`
<!-- toc -->
<!-- more -->

# 1. 环境变量,加载顺序为：

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

# 2. 语法

## 2.1. export命令

用法： export 变量名=变量值
举例：export 设置一个新的环境变量 export HELLO="hello" (可以无引号)

直接使用export命令在当前终端下声明环境变量，关闭Shell终端失效。

## 2.2. Linux中常见的环境变量

HOME：指定用户的主工作目录（即用户登陆到Linux系统中时，默认的目录）。
HOSTNAME：指主机的名称，许多应用程序如果要用到主机名的话，通常是从这个环境变量中来取得的
LOGNAME：指当前用户的登录名。
HOSTNAME：指主机的名称，许多应用程序如果要用到主机名的话，通常是从这个环境变量中来取得的
SHELL：指当前用户用的是哪种Shell。

## 2.3. PATH环境变量

```bash
# 语法，中间用冒号隔开
export PATH=$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N>
# 举例
export PATH=$PATH:/opt/local/bin:/opt/local/sbin
```

## 2.4. source配置立即生效，否则就关闭终端重新打开

```
source ~/.bash_profile
```

## 2.5. echo查看是否生效

```
echo $PATH
```

## 2.6. env 显示所有环境变量

# 3. 详细设置环境变量

## 3.1. 全局设置

## 3.2. 方法一：编辑/etc/profile文件，对所有用户生效（永久的）

添加CLASSPATH变量
```
vim /etc/profile
export CLASSPATH=./JAVA_HOME/lib;$JAVA_HOME/jre/lib
```
注：修改文件后要想马上生效还要运行source /etc/profile不然只能在下次重进此用户时生效。

## 3.3. 方法二：编辑`/etc/paths`

```
sudo vi /etc/paths
```
编辑 paths，将环境变量添加到 paths 中。
小技巧：输入环境变量时，不用一个一个地输入，只要拖动文件夹到 Terminal 里就可以了。

## 3.4. 方法三：编辑`/etc/paths.d/name`

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

## 3.5. 单个用户设置， .bash_profile 对单一用户生效（永久的）

打开 用户目录

注意： **Mac 是 .bash_profile 而Linux 里面一般设置的是 .bashrc**

```bash
cd ~
# Linux 里面是 .bashrc, mac可以使用 open -e .bash_profile 弹出可视化编辑窗口
vim ~/.bash_profile

# 把下面命令添加到上面的文件
export PATH="/Users/mashangxue/anaconda3/bin:$PATH"

# 查看PATH
echo $PATH
```

举例：添加CUDN环境变量，新建LD_LIBRARY_PATH变量
```bash
# 打开`~/.bashrc`,编辑文件 
mark@mashangxue123.com:~/TF/cuDNN$ vi ~/.bashrc

#添加下面的内容:

PATH=$PATH:/usr/local/cuda-8.0/bin
LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/usr/local/cuda/lib64:/usr/local/cuda/extras/CUPTI/lib64"
export CUDA_HOME=/usr/local/cuda
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuDNN/lib64
LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuDNN/include

```

参考文献：
[Linux环境变量总结](http://www.jianshu.com/p/ac2bc0ad3d74)
[Mac添加环境变量全面解读 ](http://blog.csdn.net/jackuhan/article/details/51868395)
[MAC 设置环境变量PATH 和 查看PATH](http://www.jianshu.com/p/acb1f062a925)