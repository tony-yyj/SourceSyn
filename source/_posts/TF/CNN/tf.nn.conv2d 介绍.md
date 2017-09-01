---
title: 卷积函数tf.nn.conv2d
tags:
  - 深度学习
categories: Tensorflow
abbrlink: 3493536208
date: 2017-09-01 17:10:10
---

<!-- toc -->
<!-- more -->

# 1. tf.nn.conv2d

在TensorFlow 的程序中加入卷积层是非常容易的。最常用的方法是 `tf.nn.conv2d`方法，用于在计算图中加入2D 卷积算子。简单的用法如下：

```
tf.nn.conv2d(input, filter, strides, padding, use_cudnn_on_gpu=None, data_format=None,name=None)
```
# 2. 参数

除去name参数用以指定该操作的name，与方法有关的一共五个参数：

- 第一个参数input：需要做卷积的输入图像，它要求是一个Tensor，具有`[batch, in_height, in_width, in_channels]` 这样的shape，具体含义是 [训练时一个batch的图片数量, 图片高度, 图片宽度, 图像通道数]，注意这是一个4维的Tensor，要求类型为float32和float64其中之一

- 第二个参数filter：卷积核大小，它要求是一个Tensor，具有`[filter_height, filter_width, in_channels, out_channels]`这样的shape，具体含义是[卷积核的高度，卷积核的宽度，图像通道数，卷积核个数]，要求类型与参数input相同,filter的通道数要求与input的in_channels一致，有一个地方需要注意，第三维in_channels，就是参数input的第四维

- 第三个参数strides：表示步长，卷积时在图像每一维的步长，这是一个一维的向量，长度4，`strides[0]=strides[3]=1`

- 第四个参数padding：表示边界的处理方式，string类型的量，只能是"SAME","VALID"其中之一，这个值决定了不同的卷积方式. 有效填充,边缘填充

- 第五个参数：use_cudnn_on_gpu:bool类型，是否使用cudnn加速，默认为true

- data_format: string类型的量 "NHWC", "NCHW"， 默认为"NHWC"。指定输入输出数据格式，默认格式为"NHWC", 数据按这样的顺序存储： `[batch, in_height, in_width, in_channels]`,也可以用这种方式："NCHW", 数据按这样的顺序存储： `[batch, in_channels, in_height, in_width]`

- 结果返回一个Tensor，这个输出，就是我们常说的feature map,type与input相同

# 3. 边界填充padding

当卷积核与图像重叠时，它应当落在图像的边界内。有时，两者尺寸可能不匹配，一种较好的补救策略是对图像缺失的区域进行填充，即边界填充。

TensorFlow会用0进行边界填充，或当卷积核与图像尺寸不匹配，但又不允许卷积核跨越图像边界时，会引发一个错误。
tf.nn.conv2d的零填充数量或错误状态是由参数padding控制的，它的取值可以是SAME或VALID。

- ·SAME：卷积输出与输入的尺寸相同。这里在计算如何跨越图像时，并不考虑滤波器的尺寸。选用该设置时，缺失的像素将用0填充，卷积核**扫过的像素数将超过图像的实际像素数**。

- ·VALID：在计算卷积核如何在图像上跨越时，需要**考虑滤波器的尺寸**。这会使卷积核尽量不越过图像的边界。在某些情形下，可能边界也会被填充。

在计算卷积时，最好能够考虑图像的尺寸，如果边界填充是必要的，则TensorFlow会有一些内置选项。在大多数比较简单的情形下，SAME都是一个不错的选择。当指定跨度参数后，如果输入和卷积核能够很好地工作，则推荐使用VALID。关于这两个参数的更多介绍，请参考

https://www.tensorflow.org/api_guides/python/nn#convolution

# 4. 数据格式data_format

tf.nn.conv2d文档详细解释了如何修改data_format(数据格式)，以使input、kernel和strides遵循某种与到目前为止所使用的格式不同的格式。

如果有某个输入张量未遵循`[batch_size，height，width，channel]`标准，则修改该格式便非常有用。除了修改输入的格式，使之与标准匹配外，也可修改data_format参数以使用一种不同的布局。

data_format：该参数可取为“NHWC”或“NCHW”，默认值为“NHWC”，用于指定输入和输出数据的格式。
- 当取默认格式“NHWC”时，数据的存储顺序为[batch，in_height，in_width，in_channels]。
- 若该参数取为“NCHW”，数据存储顺序为[batch，in_channels，in_height，in_width]。

数据格式定义：
- N  批数据中的张量数目．即batch_size
- H  每个批数据中张量的高度
- W  每个批数据中张量的宽度
- C  每个批数据中张量的通道数