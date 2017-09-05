---
title: 使用Anaconda安装tensorflow
tags:
  - Linux
  - Tensorflow
  - python
categories: Linux
date: 2017-09-05 19:18:00
---

<!-- toc -->
<!-- more -->

# 1. 创建新虚拟环境，命名为tensorflow-cpu-conda

```
conda create -n tensorflow-cpu-conda python=3.6 ipykernel
```

# 2. 进入新环境

```
source activate tensorflow-cpu-conda
```

# 3. 把这个环境安装到ipykernel，用于jupyter notebook。

```
python -m ipykernel install --user --name tensorflow-cpu-conda
```

# 4. 安装TensorFlow

```
pip install --ignore-installed --upgrade  https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.3.0-cp36-cp36m-linux_x86_64.whl

```
链接可以替换为自己下载的本地whl文件。

也可以使用conda安装
```
conda install -c anaconda tensorflow-cpu=1.1.0
```
这里的方法是搜索“conda install tensorflow cpu”之后，在conda官网https://anaconda.org/anaconda/tensorflow-gpu 这个链接找到的。

# 5. 测试安装

命令行输入python，进入Python后，执行下面的命令。

```
>>> import tensorflow as tf
>>> hello = tf.constant('Hello, TensorFlow!')
>>> sess = tf.Session()
>>> print(sess.run(hello))
```