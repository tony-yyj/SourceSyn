---
title: 风格迁移神经网络
tags:
  - 深度学习
  - Tensorflow项目
categories: Tensorflow
abbrlink: 1847235949
date: 2017-09-11 21:00:00
---

<!-- toc -->
<!-- more -->

# 1. 核心思路

- 使用现成的识别网络，提取图像不同层级的特征
- 低层次响应描述图像的风格，高层次响应描述图像的内容。
- 使用梯度下降方法，可以调整输入响应，在特定层次获得特定的响应。
- 多次迭代之后，输入响应即为特定风格和内容的图像。

利用已经训练好的权重，获取一个符合输出要求的输入。

图像风格转移
* 一天内的光照变化，不同天气的变化，四季变化 
* 与背景相容的物体风格变化 
这里指的是图像风格转移，并没有包含优化抠图与图像分割产生的效果

# 2. 卷积神经网络的可视化

一般而言，越多的卷积步骤，网络可以学到的识别特征就越复杂。比如，ConvNet 的图像分类可能在第一层从原始像素中检测出边缘，然后在第二层使用边缘检测简单的形状，接着使用这些形状检测更高级的特征，比如更高层的人脸。下面的图中展示了这些内容——我们使用 卷积深度置信网络 学习到的特征，这张图仅仅是用来证明上面的内容（这仅仅是一个例子：真正的卷积滤波器可能会检测到对我们毫无意义的物体）。

![](http://static.open-open.com/lib/uploadImg/20161025/20161025154923_163.png)


# 3. VGG网络在风格和内容量化提取中的作用

![](http://images2015.cnblogs.com/blog/1092165/201701/1092165-20170120214534593-1057568536.jpg)

如上，a有个别名是conv1_1，b是conv2_1，依次类推，c，d，e对应conv3_1，conv4_1，conv5_1；输入图片有风格图片style image和内容图片content image，输出的是就是合成图片，然后用合成图片为指导训练，但是训练的对象不像是普通的神经网络那样训练权值w和偏置项b，而是训练合成图片上的像素点，以达到损失函数不断减少的效果。论文使用的是随机的噪声像素图为初始合成图，但是使用原始图片会快一点。

网络不同层次的响应描述了图像不同层次的信息：低层次描述小范围的边角、曲线，中层次描述方块、螺旋，高层次描述内容。
浅层更注重纹理细节，深层更注重大片的图案。 

## 3.1. 量化表示“绘画风格”

“绘画风格”是一个抽象定型的词语，它可能和图像的某种高阶统计量相关，但不同的绘画风格有不同的表示，对于一个没有具体定义风格的一般性问题，它很难用人工设计算法去完成。

幸运的是，我们知道卷积网络CNN可以通过多层卷积提取物体的抽象特征完成物体识别，这一点“**提取抽象特性**”的能力被作者借用来**描述“风格**”。也就是说，经过多层CNN抽象之后的图片丢弃了像素级的特征，而保留了高级的绘画风格。

图引用自原论文图1。在文章里，作者定义了一个5层的CNN网络，梵高的星空在通过第一二三层的时候保留了一些原图的细节，但是在第四第五层的时候，就变成了“看起来是梵高星空的样子”这样的**抽象特征**。

这时候作者机智的想到了，如果把一张梵高一张其他照片同时都放到这个CNN网络里，经过合适的调整让第二张照片在第四五层接近梵高，而第一二三层保持和原来差不多，那就可以模仿梵高了！细节上，作者为了沿用了CNN的特征抽象能力**使用了**CNN作物体识别的**VGG模型**。

## 3.2. 学习风格并生成图像

于是让机器模仿绘画风格并生成图片成了一个优化问题：生成的图像要像原内容图，比如我给一张猫的图片最终还是要像猫；生成的图像要像是由风格图画的，比如我给了个梵高的图，我生成的猫的图片要看起来有梵高的风格。

也就是说要找到这样一个中间结果，它的内容表示（第一二三层CNN）接近于猫，它的风格的表示（第四第五层CNN）接近于梵高。

在文章里，作者用一个白噪声图片通过梯度下降生成一个接近内容图的图片，以及另一个白噪声图片生成一个接近绘画图风格的图片。

同时**定义了神奇的描述纹理的格拉姆矩阵 `gram matrix`，定义了这两个图的损失函数并加权平均当作优化目标函数**，在mxnet的实现里通过梯度下降（SGD）完成收敛找到这样一个内容和风格都搭配中间结果。

举例来说，“猫”和“梵高自画像”的生成过程的200多步的循环里，图像的变化依次如下图所示：

## 3.3. 风格层
和直觉相反，风格误差可以包含非常高的卷积层(conv5_1)，反而有更自然，更“神似”的视觉效果。
这告诉我们：风格本身也是非常抽象的概念，需要较深的网络来描述。

## 3.4. 合成过程
通过将a图的style和p图的content进行融合，得到第三幅图x。style+content=styled content 

![](http://img.blog.csdn.net/20160112111456945)

## 3.5. 内容损失和风格损失 两个loss

首先他定义了两个loss，分别表示最终生成的图x和style。图a的样式上的loss，以及x和content图p的内容上的loss，α,β是调节两者比例的参数。最终的loss function是两者的加和。通过optimize总的loss求得最终的x。 

![](http://img.blog.csdn.net/20160112111525420)

要注意的是，不同于一般的CNN优化，这里优化的参数不再是网络的w和b，而是初始输入的一张噪声图片x 

# 4. 最优化问题

风格转移问题：是利用CNN生成一张新图像，内容和输入图像一样，风格和想要变成的风格的参考图像一致；也可以将这个问题理解成最优化问题进行数学表示；

最优化两个图像之间的内容差别： 

图像内容差异最小化为：卷积神经网络中某层滤波后的结果的差的平方的平均值；

最优化两个图像之间的风格差别： 

图像风格差异最小化为：卷积神经网络中某层滤波后的结果的差的平方的平均值；其中的格莱姆矩阵是表示图像特征的向量之间的內积。向量內积的几何意义可以理解为两个向量在方向上的接近程度。

# 5. 色彩空间仿射变换

- 1 . 输出图像在局部出现扭曲 (为什么会扭曲，真相不明？风格变换导致的扭曲？)
- 2 . 如果是风格转移导致扭曲，将变换约束在色彩空间上；全局色彩变换使用空间不变转移函数，处理全局颜色平移，调整色调曲线（高低对比度）。可以用色彩概率分布函数，可以用直方图类比，但这些方法不能处理复杂的风格。如果要进行整体强烈变化，比如摩天大楼几个房间灯光点亮，但又不能扭曲局部几何空间。
- 3 . 局部风格变换：对新建的图像进行局部仿射色彩变换约束，防止扭曲；在构建新图像的过程中，需要从输入图像中获取内容，从参考图像中取得风格，在这个过程中要最小化内容和内容的差别、风格和风格的差别；同时要防止图像局部扭曲，引入**局部线性模型的拉普拉斯抠图代价函数作为正则项**作为修正。
- 4 . 局部线性拉普拉斯抠图代价函数，是输入图像与输出图像向量化的矩阵乘积。 

# 6. 拉普拉斯抠图

抠图，是将任何一个需要的物体无缝插入到一个指定的背景中, 当然也可以将电影演员融入到计算机所绘制的虚拟场景中去。实践中，通用的抠图技术是将用户感兴趣的部分（前景部分）从图像其他部分中分离出来的数字图像处理技术，比如著名的蓝屏抠像, 它需要将那些待抠取的物体置于蓝色或者绿色背景前面, 具有很大的局限性。

自然图像抠像主要分为三类：基于采样的方法，基于传播的方法，采样与传播相结合的方法。 

- 基于采样的方法需要用户给出较为精确的三分图, 然后对于未知区域的像素的一些抠像参数, 通过利用附近的样本来近似求得. 该方法的优点是计算速度快, 缺点是需要较为精确的三分图, 并且当采样不准确时会得到较差的抠像结果, 因此鲁棒性不强。
- 基于传播的方法 一般只需要用户给出简单的前景和背景指示线条, 然后通过某种方式将信息传播到附近的像素. 该方法的优点是只需要用户提供粗糙的三分图, 并且该方法对大部分的图片均能获得较好的抠像效果, 因此具有较强的鲁棒性. 缺点是部分先验信息浪费, 好的传播方法的设计较为困难, 计算速度慢. 采样与传播相结合的方法是目前研究的热点, 它能够有效结合前两类方法的优点, 但当采用的采样方法以及传播方法不好时, 它也会遗传前两类方法的缺点.
- 采样与传播相结合的方法通常将抠像问题转换为**能量函数最小化问题**, 能量函数由两部分构成, 一部分为数据能量项, 另外一个部分为光滑能量项, 求解图像的前景掩码层a的一般数学模型如下： 

根据Es和E的构造方法的不同, 基于采样与传播相结合的抠像方法有多种。

能量函数也就是损失函数，在抠图里面就是希望前景颜色和背景颜色差异最小化，利用最小化问题求出不透明度值。继而得到前景颜色和背景颜色。图像可以表示成多个图层的合成；每个图层的系数为该层的掩码，这个掩码是稀疏的，图像中的每个像素只受少数几个层的影响，只有少部分像素由多个不同层混合而成。 掩码与拉普拉斯矩阵特征向量之间是线性变换。 这个线性变换矩阵就是不同图像层之间的连通块，由像素子集构成。

拉普拉斯抠图矩阵，可以简单理解为**像素之间是否联通的关联矩阵**。

图像抠图算法假设每个像素由前景颜色和背景颜色线性合成，参数为不透明值α。对毛发，烟雾，火焰等无法用单像素表达或半透明的物体，图像抠图相比图像分割有明显优势。

# 7. 图像语义分割

采用图像语义分割，因为Gram Matrix 对神经元响应值进行了编码，限制了语义内容变化，导致风格“溢出”。 
因此，用语义分割算法，对输入图像和风格参考图像生成图像分割遮罩。将遮罩添加到输入图像上作为另外一个通道，增强CNN中的风格算法。
语义分割增强的风格损失函数 

# 8. 快速风格迁移神经网络

论文
https://web.stanford.edu/class/cs331b/projects/tam.pdf

# 9. 完整示例代码运行

TensorFlow (Python API) implementation of Neural Style

[cysmith/neural-style-tf](https://github.com/cysmith/neural-style-tf)

python neural_style.py --content 1-content.jpg --styles 1-style.jpg --output 1-out.jpg

模型imagenet-vgg-verydeep-19.mat下载
[Getting Title at 46:12](http://www.vlfeat.org/matconvnet/pretrained/#downloading-the-pre-trained-models)
必须是这个才可以正常运行，下载链接：
http://www.vlfeat.org/matconvnet/models/beta16/imagenet-vgg-verydeep-19.mat

# 10. 主要的开源项目：

TensorFlow CNN for fast style transfer! ⚡
++ https://github.com/lengstrom/fast-style-transfer

Neural style in TensorFlow!
https://github.com/anishathalye/neural-style

TensorFlow (Python API) implementation of Neural Style
https://github.com/cysmith/neural-style-tf

TensorFlowBook
https://github.com/DeepVisionTeam/TensorFlowBook/tree/master/neural_style

Feedforward style transfer
https://github.com/jcjohnson/fast-neural-style

论文：
A Neural Algorithm of Artistic Style
https://arxiv.org/pdf/1508.06576v2.pdf

Perceptual Losses for Real-Time Style Transfer  and Super-Resolution
https://arxiv.org/pdf/1603.08155v1.pdf
http://cs.stanford.edu/people/jcjohns/eccv16/

Image Style Transfer Using Convolutional Neural Networks
http://www.cv-foundation.org/openaccess/content_cvpr_2016/papers/Gatys_Image_Style_Transfer_CVPR_2016_paper.pdf

[https://web.stanford.edu/class/cs331b/projects/tam.pdf](https://web.stanford.edu/class/cs331b/projects/tam.pdf)

# 11. 参考文献：

[TensorFlow之深入理解Neural Style-小石头的码疯窝](http://hacker.duanshishi.com/?p=1651)

[TensorFlow之深入理解Fast Neural Style-小石头的码疯窝](http://hacker.duanshishi.com/?p=1693)

[自然图像抠图技术综述](https://wenku.baidu.com/view/b99fa83b7275a417866fb84ae45c3b3567ecddee.html)
闭合型抠图的研究与应用

[++用MXnet实战深度学习之二:Neural art ](http://www.infoq.com/cn/articles/use-mxnet-in-deep-learning-part02)

[A Neural Algorithm of Artistic Style 图像风格转换 - keras简化版实现](http://www.cnblogs.com/mangoyuan/p/6329410.html)

[【每个人都是梵高】A Neural Algorithm of Artistic Style](http://blog.csdn.net/elaine_bao/article/details/50502929)

[深度学习应用在哪些领域让你觉得「我去，这也能行！」？ - 知乎](https://www.zhihu.com/question/47563637/answer/106708095)

[神经网络的直观解释 - OPEN 开发经验库](http://www.open-open.com/lib/view/open1477381764769.html)

[量化表示“绘画风格”](http://blog.csdn.net/u011534057/article/details/51911562?locationNum=2&fps=1)

[深度卷积网络图像风格转移（一）需求分析 ](http://blog.csdn.net/cicibabe/article/details/71242813)

[深度卷积网络图像风格转移（二）架构分析 -](http://blog.csdn.net/cicibabe/article/details/72366873)

[Pretrained CNNs - MatConvNet](http://www.vlfeat.org/matconvnet/pretrained/#downloading-the-pre-trained-models)

[Ubuntu 15.04 安装TensorFlow（源码编译） 及测试梵高作画](http://blog.csdn.net/jiandanjinxin/article/details/64907373)

