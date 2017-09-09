---
title: OpenCV HOG+SVM行人检测
tags:
  - opencv
  - opencv教程
categories: opencv
abbrlink: 1063667049
date: 2017-09-09 15:00:00
---

<!-- toc -->
<!-- more -->

# 1. 行人检测介绍

行人检测，就是将一张图片中的行人检测出来，并输出bounding box级别的结果。而如果将各个行人之间的轨迹关联起来，就变成了行人跟踪。而行人检索则是把一段视频中的某个感兴趣的人检索出来。

在2005年CVPR上，来自法国的研究人员Navneet Dalal 和Bill Triggs提出利用**Hog进行特征提取，利用线性SVM作为分类器**，从而实现行人检测。

## 1.1. HOG算子

梯度直方图特征(HOG) 是一种对图像**局部重叠区域**的密集型描述符, 它通过**计算局部区域上的梯度方向直方图**来构成人体特征,能够很好地描述人体的边缘。它对光照变化和小量的偏移不敏感。
 参考： [HOG算子 - 计算机视觉小菜鸟的专栏- CSDN博客](http://blog.csdn.net/carson2005/article/details/7782726)

## 1.2. SVM

支持向量机SVM是从线性可分情况下的最优分类面提出的。所谓最优分类，就是要求分类线不但能够将两类无错误的分开，而且两类之间的分类间隔最大，前者是保证经验风险最小（为0），而通过后面的讨论我们看到，使分类间隔最大实际上就是使得推广性中的置信范围最小。推广到高维空间，最优分类线就成为最优分类面。

SVM使用的是OpenCV自带的CvSVM类。
参考：[支持向量机简介 - 计算机视觉小菜鸟的专栏   - CSDN博客](http://blog.csdn.net/carson2005/article/details/6453502)

# 2. HOG+SVM行人检测

首先计算样本图像的HOG描述子，组成一个特征向量矩阵，对应的要有一个指定每个特征向量的类别的类标向量，输入SVM中进行训练，训练好的SVM分类器保存为XML文件，
然后根据其中的支持向量和参数生成OpenCV中的HOG描述子可用的检测子参数，再调用OpenCV中的多尺度检测函数进行行人检测。

现在利用HOG特征来进行行人检测，既然要有了特征，现在其实要有一个方法来判断是否一个图片的某一部分是行人，SVM是一个很好的机器学习方法，可以用来分类，结合HOG特征就可以用来检测图片中的行人。OpenCV中集成了一个方法，getDefaultPeopleDetector等可以直接得到一个SVM的分类器，这个分类器是OpenCV自带的已经训练好的，可以直接拿来使用。下面可以看一下使用它的代码。

     
## 2.1. HOGDescriptor类的构造函数的各参数的定义：

cv::HOGDescriptor

```c++
CV_WRAP HOGDescriptor() :   
     winSize(64,128),          // detect window   
     blockSize(16,16),         // block 大小   
     blockStride(8,8),         // overlap block的滑动步长   
     cellSize(8,8),            // cell 大小    
     nbins(9),                 // 直方图的bin个数   
     derivAperture(1),          // 微分算子核   
     winSigma(-1),              // 在window上进行高斯加权   
     histogramNormType(HOGDescriptor::L2Hys), // 直方图归一化类型   
     L2HysThreshold(0.2),  
     // L2-norm followed by clipping (limiting the maximum values of v to 0.2) and renormalising 
     gammaCorrection(true), // Gamma校正，去除光照影响  
     nlevels(HOGDescriptor::DEFAULT_NLEVELS)   // 分层数  

```

## 2.2. HOG多尺度检测函数detectMultiScale

void detectMultiScale(constGpuMat& img, vector<Rect>& found_locations, double hit_threshold= 0,
                                       Sizewin_stride = Size(), Size padding = Size(), double scale0=1.05,intgroup_threshold=2 );

```c++
void detectMultiScale(constGpuMat& img, vector<Rect>& found_locations, double hit_threshold= 0,
                                       Sizewin_stride = Size(), Size padding = Size(), double scale0=1.05,intgroup_threshold=2 );
```

- img：待检测的图像，支持CV_8UC1或CV_8UC4类型
- found_locations：检测到的目标的包围框数组
- hit_threshold：检测到的特征到SVM分类超平面的距离，一般是设为0，在分类器参数中指明。
- win_stride：检测窗口每次移动的距离，必须是块移动的整数倍
- padding：保持CPU接口兼容性的虚参数，必须是(0,0)。但网上下载的例子里是(32,32)
- scale0：滑动窗口每次增加的比例
- group_threshold：组阈值，即校正系数，当一个目标被多个窗口检测出来时，该参数此时就起了调节作用， 为0时表示不起调节作用。

# 3. 示例代码：

```c++
#include <iostream>  
#include <string>  
#include <opencv2/core/core.hpp>  
#include <opencv2/highgui/highgui.hpp>  
#include <opencv2/imgproc/imgproc.hpp>  
#include <opencv2/objdetect/objdetect.hpp>  
#include <opencv2/ml/ml.hpp>  

using namespace std;
using namespace cv;

int mainHog()
{
    Mat src = imread("5.jpg");
    // 1. 定义HOG对象  
    HOGDescriptor hog;//HOG特征检测器  
    // 2. 设置SVM分类器  
    hog.setSVMDetector(HOGDescriptor::getDefaultPeopleDetector());//设置SVM分类器为默认参数  
    // 3. 在测试图像上检测行人区域
    vector<Rect> found, found_filtered;//矩形框数组  
    hog.detectMultiScale(src, found, 0, Size(8, 8), Size(32, 32), 1.05, 2);//对图像进行多尺度检测，检测窗口移动步长为(8,8)  

    cout << "矩形个数：" << found.size() << endl;
    //4.找出所有没有嵌套的矩形框r,并放入found_filtered中,如果有嵌套的话,则取外面最大的那个矩形框放入found_filtered中  
    for (int i = 0; i < found.size(); i++)
    {
        Rect r = found[i];
        int j = 0;
        for (; j < found.size(); j++)
            if (j != i && (r & found[j]) == r)
                break;
        if (j == found.size())
            found_filtered.push_back(r);
    }
    cout << "过滤后矩形的个数：" << found_filtered.size() << endl;

    //5.画矩形框，因为hog检测出的矩形框比实际人体框要稍微大些,所以这里需要做一些调整
    for (int i = 0; i<found_filtered.size(); i++)
    {
        Rect r = found_filtered[i];
        r.x += cvRound(r.width*0.1);
        r.width = cvRound(r.width*0.8);
        r.y += cvRound(r.height*0.07);
        r.height = cvRound(r.height*0.8);
        rectangle(src, r.tl(), r.br(), Scalar(0, 255, 0), 3);
    }
    imwrite("ImgProcessed.jpg", src);
    namedWindow("src", 0);
    imshow("src", src);
    waitKey();
    system("pause");
    return 0;
}
```

# 4. 参考：

[论文： 用于人体检测的方向梯度直方图](http://blog.csdn.net/masibuaa/article/details/14056807)

[利用Hog特征和SVM分类器进行行人检测 - 计算机视觉小菜鸟的专栏  - CSDN博客](http://blog.csdn.net/carson2005/article/details/7841443)

[Opencv HOG行人检测 源码分析(一) - Note of Transposition  - CSDN博客](http://blog.csdn.net/ttransposition/article/details/11874285)

[opencv︱opencv中实现行人检测：HOG+SVM（二） - CSDN博客](http://blog.csdn.net/sinat_26917383/article/details/69666505)

[HOG+SVM行人检测opencv版本 - 一呆飞仙的博客- CSDN博客](http://blog.csdn.net/l297969586/article/details/53099873)

[用初次训练的SVM+HOG分类器在负样本原图上检测HardExample - CSDN博客](http://blog.csdn.net/masibuaa/article/details/16113373)
  
[目标检测—HOG特征和OpenCV中的实现 - ZH de 部落格  - CSDN博客](http://blog.csdn.net/zhonghuan1992/article/details/38789943)

[OpenCV HOGDescriptor 参数图解 CSDN博客](http://blog.csdn.net/raodotcong/article/details/6239431)
