---
title: 安装CUDA Toolkit 并行计算架构
tags:
  - Linux
  - Tensorflow
  - CUDA
categories: Linux
abbrlink: 2141991750
date: 2017-09-05 18:18:00
---

<!-- toc -->
<!-- more -->

CUDA(Compute Unified Device Architecture)，是显卡厂商NVIDIA推出的运算平台。 CUDA™是一种由NVIDIA推出的通用并行计算架构，该架构使GPU能够解决复杂的计算问题。 CUDA的安装包里一般集成了显卡驱动
# 1. 检查是否有GPU

命令：`lspci | grep -i nvidia`

输出内容：

```bash
mark@mashangxue123.com:~$ lspci | grep -i nvidia
04:00.0 VGA compatible controller: NVIDIA Corporation Device 1b02 (rev a1)
04:00.1 Audio device: NVIDIA Corporation Device 10ef (rev a1)
05:00.0 VGA compatible controller: NVIDIA Corporation Device 1b02 (rev a1)
05:00.1 Audio device: NVIDIA Corporation Device 10ef (rev a1)
08:00.0 VGA compatible controller: NVIDIA Corporation Device 1b02 (rev a1)
08:00.1 Audio device: NVIDIA Corporation Device 10ef (rev a1)
09:00.0 VGA compatible controller: NVIDIA Corporation Device 1b02 (rev a1)
09:00.1 Audio device: NVIDIA Corporation Device 10ef (rev a1)

```

# 2. 查看系统内核`uname -r`
```
mark@mashangxue123.com:~$ uname -r
4.10.0-30-generic
```

# 3. 安装内核头文件
```
sudo apt-get install linux-headers-$(uname -r)
```

# 4. 获取deb安装包地址

在cuda工具箱下载页面 https://developer.nvidia.com/cuda-downloads
依次选择“Linux, x8664, Ubuntu, 16.04， deb (network)”。然后复制下面出现的下载图标的下载地址（右键，“复制链接地址”）。
其地址是 https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb

# 5. 下载这个文件到服务器

回到命令行输入

```bash
mark@mashangxue123.com:~$ wget  https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
.....
Length: 2690 (2.6K) [application/x-deb]
Saving to: ‘cuda-repo-ubuntu1604_8.0.61-1_amd64.deb’

cuda-repo-ubuntu1604_8.0.61-1_amd64.deb            100%[==============================================================================================================>]   2.63K  --.-KB/s    in 0s      

 ‘cuda-repo-ubuntu1604_8.0.61-1_amd64.deb’ saved [2690/2690]

```

# 6. 安装cuda

在命令行中依次输入下面的命令后，等待安装完成

```bash
sudo dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

提示需要你的确认，输入Y按回车确认。

当看到下面的输出时，就代表安装完成了。

```bash
done.
done.
roden@ip-172-31-19-170:~/download$
```

# 7. 重启系统

否则会出错“Driver/library version mismatch”
如果不想重启可以参考这篇文章解决 
“https://comzyh.com/blog/archives/967/” [解决Driver/library version mismatch | Comzyh的博客](https://comzyh.com/blog/archives/967/)

# 8. 查看GPU的使用情况 `nvidia-smi`
`nvidia-smi`命令只有在完成了cuda的安装后才有效;
在使用GPU训练模型是，我们可以再次使用这个命令看看结果。

```bash
mark@mashangxue123.com:~$ nvidia-smi
Tue Sep  5 10:50:56 2017
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 384.66                 Driver Version: 384.66                    |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  TITAN Xp            Off  | 00000000:04:00.0 Off |                  N/A |
| 23%   28C    P8     8W / 250W |    175MiB / 12189MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   1  TITAN Xp            Off  | 00000000:05:00.0 Off |                  N/A |
| 23%   24C    P8     9W / 250W |     10MiB / 12189MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   2  TITAN Xp            Off  | 00000000:08:00.0 Off |                  N/A |
| 23%   24C    P8     8W / 250W |     10MiB / 12189MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   3  TITAN Xp            Off  | 00000000:09:00.0 Off |                  N/A |
| 23%   28C    P8     8W / 250W |     10MiB / 12189MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID  Type  Process name                               Usage      |
|=============================================================================|
|    0      1914    C   /usr/bin/python                                165MiB |
+-----------------------------------------------------------------------------+

```
显卡是NVIDIA TITAN Xp ，官方链接[NVIDIA TITAN Xp Graphics Card with Pascal Architecture](https://www.nvidia.com/en-us/geforce/products/10series/titan-xp/)
这款坐上高端消费市场新卡皇位子的产品，是基于 Pascal GP102 芯片打造（Quadro P6000 同款）。它搭载了 3,840 颗「满血」CUDA 核心（1080 Ti 是 3,584 颗），同时拥有跟 Titan X 一样 12GB GDDR5X 内存，不过后者的频率从 10GHz 的基础上提升到了 11.4GHz，频宽也相应从 480GB/s 增加到了 547.7GB/s。

# 9. 配置LD_LIBRARY_PATH环境变量
如果GPU环境下加载tensorflow时,遇上找不到cuda库的问题时，很简单，需要配置LD_LIBRARY_PATH环境变量。

在~/.bashrc中添加：
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-8.0/lib64/
```
或者在打开python或ipython前在shell中执行:
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-8.0/lib64/
```
这里假设将cuda库安装于/usr/local/cuda-8.0/lib64/中。里边包括 libcudnn.so等动态链接库文件。

[亚马逊云教程7：安装支持GPU的TensorFlow](http://aws.cn.riverlight.blog/aws/2017/06/12/AWS_tutorial_7.html)
[TensorFlow 起飞之旅 · 安装 · demo - 个人文章 - SegmentFault](https://segmentfault.com/a/1190000010081525)