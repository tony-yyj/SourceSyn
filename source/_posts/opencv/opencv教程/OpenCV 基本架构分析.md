---
title: OpenCV 基本架构分析
tags:
  - opencv
  - opencv教程
categories: opencv
abbrlink: 277275245
date: 2017-09-09 11:00:00
---

<!-- toc -->
<!-- more -->

# 1. 所有组件的宏opencv_mod ules.hpp 

进入到 `\opencv\build\include` 目录，可以看到有opencv 和opencv2 这两个文件夹:
- opencv 里面包含着旧版的头文件，
- opencv2 里面包含着具有时代意义的新版OpenCV2 系列的头文件。

重点关注的opencv2 文件夹，在 `＼opencv\build\include\opencv2` 目录有个名为 `opencv_mod ules.hpp` 的hpp 文件，里面存放的是 OpenCV2 中与新模块构造相关的说明代码，打开可以发现其定义的是OpenCV2 所有组件的宏， 具体如下。

```c++
#define HAVE_OPENCV_CALIB3D
#define HAVE_OPENCV_CORE
#define HAVE_OPENCV_FEATURES2D
#define HAVE_OPENCV_FLANN
#define HAVE_OPENCV_HIGHGUI
#define HAVE_OPENCV_IMGCODECS
#define HAVE_OPENCV_IMGPROC
#define HAVE_OPENCV_ML
#define HAVE_OPENCV_OBJDETECT
#define HAVE_OPENCV_PHOTO
#define HAVE_OPENCV_SHAPE
#define HAVE_OPENCV_STITCHING
#define HAVE_OPENCV_SUPERRES
#define HAVE_OPENCV_VIDEO
#define HAVE_OPENCV_VIDEOIO
#define HAVE_OPENCV_VIDEOSTAB
#define HAVE_OPENCV_WORLD
```

# 2. OpenCV 所有模块介绍:

按照上面文件中的宏定义的顺序

## 2.1. 【calib3d】 Calibration （校准〕和3D 这两个词的组合缩写。

这个模块主要是相机校准和三维重建相关的内容，包括基本的多视角几何算法、单个立体摄像头标定、物体姿态估计、立体相似性算法、3D 信息的重建等。

## 2.2. 【contrib 】 Contributed/Experimental Stuf 的缩写。

该模块包含了一些最近添加的不太稳定的可选功能， 不用去多管。新增了新型人脸识别、立体匹配、人工视网膜模型等技术。

## 2.3. 【core 】 核心功能模块，包含如下内容：
- OpenCV 基本数据结构
- 动态数据结构
- 绘图函数
- 数组操作相关函数
- 辅助功能与系统函数和宏
- 与OpenGL 的互操作
- CUDA GPU计算框架

## 2.4. 【imgproc 】 Image 和Process 这两个单词的缩写组合，图像处理模块。包含如下内容：
- 线性和非线性的图像滤波
- 图像的几何变换
- 其他（ Miscellaneous ）图像转换
- 直方图相关
- 结构分析和形状描述
- 运动分析和对象跟踪
- 特征检测
- 目标检测等内容

## 2.5. 【features2d 】也就是Features2D ，即2D功能框架，包含如下内容：
- 特征检测和描述
- 特征检测器（ Feature Detectors ）通用接口
- 描述符提取器（ Descriptor Extractors ）通用接口
- 描述符匹配器（ Descriptor Matchers ）通用接口
- 通用描述符（ Generic Descriptor ）匹配器通用接口
- 关键点绘制函数和匹配功能绘制函数

## 2.6. 【flann 】 Fast Library for Approximate Nearest Neighbors
高维的近似近邻快速搜索算法库， 包含以下两个部分：

- 快速近似最近邻搜索
- 聚类

## 2.7. 【gpu】运用GPU 加速的计算机视觉模块。

## 2.8. 【highgui】高层GUI图形用户界面,
包含媒体的输入输出、视频捕捉、图像和视频的编码解码、图形交互界面的接口等内容。

## 2.9. 【legacy】－些己经废弃的代码库，保留下来作为向下兼容，包含如下内容：

- 运动分析
- 期望最大化
- 直方图
- 平面细分 CAPI
- 特征检测和描述（ Feature Detection and Description )
- 描述符提取器(Descriptor Extractors）的通用接口
- 通用描述符（ Generic Descriptor Matchers ）的常用接口
- 匹配器

## 2.10. 【ml】 Machine Learning ，机器学习模块，基本上是统计模型和分类算法，包含如下内容：

- 统计模型（ Statistical Models )
- 一般贝叶斯分类器（ Normal Bayes Classifier)
- K-近邻 (K-Nearest Neighbors )
- 支持向量机（Support Vector Machines )
- 决策树（ Decision Trees )
- 提升（ Boosting )
- 梯度提高树（ Gradient Boosted Trees)
- 随机树（ Random Trees )
- 超随机树（ Extremely randomized trees )
- 期望最大化（ Expectation Maximization )
- 神经网络（ Neural Networks )
- MLData

## 2.11. 【nonfree】一些具有专利的算法模块，包含特征检测和GPU 相关的内容。最好不要商用。

## 2.12. 【objdetect】  目标检测模块， 包含Cascade Classification （级联分类）和 Latent SVM 这两个部分。

## 2.13. 【ocl】  OpenCL-accelerated Computer Vision ， 运用OpenCL 加速的计算机视觉组件模块。

## 2.14. 【photo】  Computational Photography， 包含图像修复和图像去噪两部分

## 2.15. 【stitching】  images stitching，图像拼接模块，包含如下部分：

- 拼接流水线
- 特点寻找和匹配图像
- 估计旋转
- 自动校准
- 图片歪斜
- 接缝估测
- 曝光补偿
- 图片混合

## 2.16. 【superres 】 Super Resolution ， 超分辨率技术的相关功能模块。

## 2.17. 【ts】 OpenCV 测试相关代码， 不用去管。

## 2.18. 【video 】视频分析组件， 该模块包括运动估计、背景分离、对象跟踪等视频处理相关内容。

## 2.19. 【Videostab 】Video stabilization ，视频稳定相关的组件，官方文档中没有多做介绍， 不用管它。

OpenCV 其实就是这么多模块作为代码容器组合起来的一个SDK (Software Development Kit 软件开发工具包)而己，并不繁杂， 也不稀奇。

# 3. OpenCV3项目架构的改变

OpenCV 3.0的出现， 就是为了给日益发福的OpenCV 减肥， 因为OpenCV3 决定像其他大项目一样，抛弃整体架构， 使用内核＋插件的架构形式。

在GitHub 中，除了存放着正式版OpenCV 的主仓库和新增加的 “opencv _extra＂仓库以外，
OpenCV 3.0 中还添加了一个名为 `opencv_contrib` 的全新仓库，这个新仓库中有很多让人兴奋的功能：包括脸部识别和文本探测，以及文本识别、新的边缘检测器、充满艺术感的图像修复、深度地图处理、新的光流和追踪算法等。

Open CV 主仓库的地址：https://github.com/opencv/opencv
opencv_extra 仓库地址： https://github.com/opencv/opencv_extra
opencv_contrib 仓库地址：https://github.com/opencv/opencv_contrib

# 4. 正式版opencv 与opencv_contrib 之间的区别如下：

- 两者都由OpenCV 官方开发团队持续集成系统维护，虽然目前opencv_contrib 仓库中的代码测试并没有完成，很多功能不稳定。
- 主体的opencv 有着非常稳定的API 以及少部分的创新。
- opencv_contrib 仓库是大多数实验性代码放置的地方, 一些API可能会有改变， 一直会欢迎广大开发者们贡献新的精彩算法。
- opencv_contrib 中的这些额外模块可以在CMake 中用OPENCY_EXTRA_MODULES PATH=/modules 传递给CMake 文件，和openCV3 主体中的代码一起编译和运行。
- opencv contrib 的文档是自动生成的， 可以在 http://docs.opencv.org/master/ 中找到， 并会在随后的版本中更加完善。
