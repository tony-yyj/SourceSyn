---
title: ILSVRC 图像识别的难题
tags:
  - 深度学习
categories: Tensorflow
abbrlink: 3743548552
date: 2017-09-01 17:00:00
---

<!-- toc -->
<!-- more -->
# 1. 图像识别的难题

ILSVRC (lmageNct Large Scale Visual Recognition Challenge ）是近年来机器视觉领域最受迫捧也是最具权威的学术竞赛之一。
每年全世界最顶尖的科学家和企业都会参与到这个盛会中，利用最前沿、最先进的算法来解决图像识别方面的难题，并不断刷新新各种挑战的记求，代表了图像领域的最高水平。几乎每一年冠军队伍提出的新模型，都是来年 CVPR 会议上的大热门。

ImageNet 数据集是 ILSVRC 竞赛中使用的数据集，由斯坦福大学著名的华人教授李飞飞主导，其中包含了超过 1400 万张全尺寸的有标记图片。

ILSVRC 比赛会每年从ImageNet 数据集中抽出部分样本，以2012 年为例，比赛的训练集包含 1281167 张图片，验证集包含 50000 张图片，测试集为100000 张图片。

在2012 年，有一个名为Super Vision 的参赛团队提交了一个富有创造性的神经网络架构的解决方案。在以往的ILSVRC 提交结果中并不乏具备创新性的解决方案，但Supervision 在图像分类任务中表现出的空前准确性使其异常出众。Super Vision 为计算机视觉的准确率建立了全新的标准，并激发了人们对一种名为卷积神经网络的深度学习技术的极大兴趣。

ILSVRC 竞赛的比赛项目实际上是图像识别和计算机视觉领域中最困难、应用范围最广、最需要解快的问题。
它包括如下几个问题：

# 2. . 图像分类与目标定位（ CLS-LOC)

图像分类与目标定位最初是两个独立的项目，
图像分类的任务是要判断图片中的物体在1000 个分类中所属的类别，主要采用top-5 错误率的评估方式，
每张图给出5 次猜测结果，只要 5 次中有一次命中真实类别就算正确分类，最后统计完全没有命中的错误率。

2012 年之前， 图像分类最好的成绩是26%的错误率， 2012 年 AlexNet 的出现降低了 10 个百分点，错误率降到16%.
而到了2016年，由公安部第三研究所选派的“搜神”（Trimps-Soushen ）代表队在这项目中获得冠年． 将成绩提高到仅有2.9%的相误率。

目标定位是要在分类正确的基础上，从图片中标识出目标物体所在的位置，用方框框定，以错误率作为评判标准。
其难度在于，图像分类问题可以有5 次尝试机会，而目标定位为题上，每一次都需要框定得非常准确。

在这一项目上，2015年 ResNet 贡献了巨大的提高，从上一年的最好成约25%的错误率， 提高到到 9%。
2016年该项目的冠军同样是公安部三所的 Trimps-Sousben 代表队，错误率仅为7.7% 。

# 3. 目标检测(DET)

目标检测是在定位的基础上更进一步， 在图片中同时检测并定位多个类别的物体。
具休来说，是要在每一张测试图片中找到属于200 个目标类别中的所有物体，如人、勺子、水杯等。
最终的评判方式是看模型在每一个单独类别中所有物体的识别准确卒，在多数类别中都获得最高准确率的队伍获胜。

平均检出率 mean AP( mean Average Precision )是这一项上的重要指标， 一般来说，平均检出率最高的队伍也会在多数的独立类别中
获胜， 2016 年这一成绩达到 66.2%。

# 4. 视频目标检测（VID）

视频目标检测与图片目标检测任务类似，是要检测出视频每一帧中包含的多个类别的物休。
要检测的目标物体有30 个类别，是目标检测200 个类别的子集。
此项问题最大的难度在于要求算法的检测效率非常高。

评判方式与目标检测相同，在独立类别识别最准确的队伍获胜。
2016 年南京信息工程大学队伍在这一项目上获得了冠军，他们提供的两个模型分别在 10 个类别中胜出，并且达到了平均检出率超过80%的好成绩。

# 5. 场景分类（ Scene)

**场景分类**是要识别图片中的场景，比如森林、剧场、会议室、商店等。也即是说，场景分类要识别图像中的背景。

这个项目由MIT Places 团队组织，使用Places2 数据集，其中包括400 多个场景的超过1000 万张图片。

评判标准与图像分类相同， 5 次猜测中有一次命中即可，最后统计错误率， 2016 年最佳成绩的错误率仅为9% 。

场景分类问题中有一个子问题是**场景分割**，是要将图片划分为不同的区域，比如天空、道路、人、桌子等。
该项目由MIT CSAIL视觉组组织，使用 ADE20K 数据集，包含 2 万多张图片， 150 个标注类别，例如天空、玻璃、人、车、床等。
这个项目会同时评估像素级准确率和分类IoU (Intersection of Union 。

除了ILSVRC 竞赛列出的题目之外，图像领域的深度学习探索还有许多有趣的问题，
比如看图说话（Image Captioning）是为给定的图片配上一段说明文宇，
图像纹理提取的是是图像中的纹理特征。
更有一些无监督学习的探索，比如 Google 让计算机自己从无标注的图片中学会了识别猫的样子。

总之，可以说图像识别是一项基础研究，应用场景非常丰富。所要面临的问题也非常有挑战，仍然需要不懈地研究下去。
