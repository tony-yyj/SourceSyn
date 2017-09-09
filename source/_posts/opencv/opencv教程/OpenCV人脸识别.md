---
title: OpenCV人脸识别
tags:
  - opencv
  - opencv教程
categories: opencv
abbrlink: 3237760228
date: 2017-09-09 14:00:00
---

<!-- toc -->
<!-- more -->

# 1. OpenCV人脸识别原理

OpenCV中有检测人脸的函数（该函数还可以检测一些其他物体）， 甚至还包含一些预先训练好的物体识别文件。所以利用这些现成的东西就可以很快做出一个人脸检测的程序。
主要步骤为：
1.加载分类器。
用cvLoad函数读入xml格式的文件。文件在OpenCV安装目录下的“data/haarcascades/”路径下。
2.读入待检测图像。读入图片或者视频。
3.检测人脸。

算法原理："Adaptive Boosting"（自适应增强）
Adaboost是一种迭代算法，其核心思想是针对同一个训练集训练不同的分类器（弱分类器），然后把这些弱分类器集合起来，构成一个更强的最终分类器（强分类器）。利用Adaboost学习算法进行特征选择和分类器训练，把弱分类器组合成强分类器。
AdaBoost方法的自适应在于：前一个分类器分错的样本会被用来训练下一个分类器，采用分类器级联提高效率。

[AdaBoost | 数据挖掘十大算法详解](https://wizardforcel.gitbooks.io/dm-algo-top10/content/adaboost.html)

# 2. 人脸的Haar特征分类器

人脸的Haar特征分类器就是一个XML文件，该文件中会描述人脸的Haar特征值。当然Haar特征的用途可不止可以用来描述人脸这一种，用来描述眼睛，嘴唇或是其它物体也是可以的。

haarcascade_frontalface_alt.xml系OpenCV自带的分类器，文件路径
`"opencv\\sources\\data\\haarcascades\\haarcascade_frontalface_alt.xml"`

OpenCV安装目录中的\data\ haarcascades目录下的haarcascade_frontalface_alt.xml与haarcascade_frontalface_alt2.xml都是用来检测人脸的Haar分类器。

这个haarcascades目录下还有人的全身，眼睛，嘴唇的Haar分类器。检测眼睛haarcascade_eye_tree_eyeglasses.xml，

如果需要检测其他部位，可以到下面网站下载相应的分类器
 http://wiki.opencv.org.cn/index.php/%e7%89%b9%e5%be%81%e6%a3%80%e6%b5%8b%e4%b8%93%e9%a2%98 

# 3. 怎么用人脸的Haar特征分类器

cvHaarDetectObjects函数中指定相应的人脸 特征检测分类器，就可以检测出图片中所有的人脸，并将检测到的人脸通过矩形的方式返回。

```c++
CVAPI(CvSeq*) cvHaarDetectObjects(  
    const CvArr* image,  
    CvHaarClassifierCascade* cascade,  
    CvMemStorage* storage,  
    double scale_factor CV_DEFAULT(1.1),  
    int min_neighbors CV_DEFAULT(3),  
    int flags CV_DEFAULT(0),  
    CvSize min_size CV_DEFAULT(cvSize(0,0)),  
    CvSize max_size CV_DEFAULT(cvSize(0,0))  
);  

CvSeq *pcvSeqFaces = cvHaarDetectObjects(pGrayImage, pHaarCascade, pcvMStorage);  

```

总共有8个参数，函数说明：
- 参数1：表示输入图像，尽量使用灰度图以加快检测速度。
- 参数2：表示Haar特征分类器，可以用cvLoad()函数来从磁盘中加载xml文件作为Haar特征分类器。
- 参数3：用来存储检测到的候选目标的内存缓存区域。
- 参数4：表示在前后两次相继的扫描中，搜索窗口的比例系数。默认为1.1即每次搜索- 窗口依次扩大10%
- 参数5：表示构成检测目标的相邻矩形的最小个数(默认为3个)。如果组成检测目标的小矩形的个数和小于 min_neighbors - 1 都会被排除。如果min_neighbors 为 0, 则函数不做任何操作就返回所有的被检候选矩形框，这种设定值一般用在用户自定义对检测结果的组合程序上。
- 参数6：要么使用默认值，要么使用CV_HAAR_DO_CANNY_PRUNING，如果设置为CV_HAAR_DO_CANNY_PRUNING，那么函数将会使用Canny边缘检测来排除边缘过多或过少的区域，因此这些区域通常不会是人脸所在区域。
- 参数7：表示检测窗口的最小值，一般设置为默认即可。
- 参数8：表示检测窗口的最大值，一般设置为默认即可。
函数返回值：函数将返回CvSeq对象，该对象包含一系列CvRect表示检测到的人脸矩形。

# 4. 人脸识别示例完整代码
```c++
// Haar特征检测 - 人脸识别  
#include <opencv2/opencv.hpp>  
#include <cstdio>  
#include <cstdlib>  
#include <Windows.h>  
using namespace std;
int mainFaceDetection(const char *filename)
{
    //1.加载Haar特征检测分类器
    const char *pstrCascadeFileName = "haarcascade_frontalface_alt.xml";
    CvHaarClassifierCascade *pHaarCascade = NULL;
    pHaarCascade = (CvHaarClassifierCascade*)cvLoad(pstrCascadeFileName);
    if(!pHaarCascade) {printf("分类器加载失败\n");return -1;}  

   //2.载入图像
    IplImage *pSrcImage = cvLoadImage(filename, CV_LOAD_IMAGE_UNCHANGED);
   // 转化成灰度图，提高检测速度
    IplImage *pGrayImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);
    cvCvtColor(pSrcImage, pGrayImage, CV_BGR2GRAY);

    //3.人脸识别与标记  
    CvScalar FaceCirclecolors[] =
    {
        { 0,   0, 255 },
        { 0, 128, 255 },
        { 0, 255, 255 },
        { 0, 255,   0 },
        { 255, 128,   0 },
        { 255, 255,   0 },
        { 255,   0,   0 },
        { 255,   0, 255 }
    };
   // 设置缓存区  
    CvMemStorage *pcvMStorage = cvCreateMemStorage(0);
    cvClearMemStorage(pcvMStorage);//用完释放使用cvReleaseMemStorage

    //3.1 识别
    DWORD dwTimeBegin, dwTimeEnd;
    dwTimeBegin = GetTickCount();
    CvSeq *pcvSeqFaces = cvHaarDetectObjects(pGrayImage, pHaarCascade, pcvMStorage);
    dwTimeEnd = GetTickCount();
    printf("人脸个数: %d   识别用时: %d ms\n", pcvSeqFaces->total, dwTimeEnd - dwTimeBegin);

    //3.2 标记 
    for (int i = 0; i <pcvSeqFaces->total; i++)
    {
        CvRect* r = (CvRect*)cvGetSeqElem(pcvSeqFaces, i);
        CvPoint center;
        int radius;
        center.x = cvRound((r->x + r->width * 0.5));
        center.y = cvRound((r->y + r->height * 0.5));
        radius = cvRound((r->width + r->height) * 0.25);
        cvCircle(pSrcImage, center, radius, FaceCirclecolors[i % 8], 2);
        // cvRectangle函数参数： 图片， 左上角， 右下角， 颜色， 线条粗细， 线条类型，点类型  
        //cvPoint(cvRound(r->x), cvRound(r->y))
        cvRectangle(pSrcImage, center, cvPoint(cvRound(r->width), cvRound(r->height)),
            FaceCirclecolors[i % 8], 1, 1, 0);
    }
    cvReleaseMemStorage(&pcvMStorage);// 释放缓存

    const char *pstrWindowsTitle = "人脸识别";
    cvNamedWindow(pstrWindowsTitle, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsTitle, pSrcImage);

    cvWaitKey(0);

    cvDestroyWindow(pstrWindowsTitle);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&pGrayImage);
    return 0;
}
```

# 5. 参考文档：

* [【OpenCV入门指南】第十三篇 人脸检测 - MoreWindows Blog](http://blog.csdn.net/morewindows/article/details/8426318)

* [特征检测专题 - OpenCV China ：图像处理,计算机视觉库,Image Processing, Computer Vision](http://wiki.opencv.org.cn/index.php/%E7%89%B9%E5%BE%81%E6%A3%80%E6%B5%8B%E4%B8%93%E9%A2%98)
* （专题详细介绍了人脸检测的原理）

* [opencv人脸识别--cvHaarDetectObjects函数 - 我不抽烟- CSDN博客](http://blog.csdn.net/itismelzp/article/details/50378468)

* [OpenCV人脸检测 - chlele0105的专栏     - CSDN博客](http://blog.csdn.net/chlele0105/article/details/11787457)

Adaboost的几个人脸检测网站
 
【1】基础学习笔记之opencv(1)：opencv中facedetect例子浅析
 http://www.cnblogs.com/tornadomeet/archive/2012/03/22/2411318.html
【2】OpenCV学习笔记（二十七）——基于级联分类器的目标检测objdect 
http://blog.csdn.net/yang_xian521/article/details/6973667
【3】Haar+Adaboost实现人头检测
 http://blackhuman.blogcn.com/archives/143
【4】AdaBoost中利用Haar特征进行人脸识别算法分析与总结1——Haar特征与积分图 
http://blog.csdn.net/weixingstudio/article/details/7631241
【5】AdaBoost中利用Haar特征进行人脸识别算法分析与总结2——级联分类器与检测过程 
http://blog.csdn.net/weixingstudio/article/details/7631949
【6】Cv模式识别
 http://www.opencv.org.cn/index.php/Cv%E6%A8%A1%E5%BC%8F%E8%AF%86%E5%88%AB
【7】OpenCV Haar分类器人脸检测部分代码注释
 http://www.haogongju.net/art/1441498
【8】浅析人脸检测之Haar分类器方法  
http://www.cnblogs.com/ello/archive/2012/04/28/2475419.html
【9】OpenCV学习笔记（三）人脸检测的代码分析
 http://blog.csdn.net/Jee44/article/details/3454528
【10】OpenCV之 HaarTraining算法剖析
 http://www.opencv.org.cn/forum/viewtopic.php?f=1&t=4650
【11】Haar Training之CreateSamples http://www.opencv.org.cn/forum/viewtopic.php?f=1&t=7706
【12】OpenCV训练分类器制作xml文档 
 http://blog.sina.com.cn/s/blog_617d698f0100xnx9.html
【13】opencv haartraining 分析一：cvCreateTreeCascadeClassifier 
http://blog.sina.com.cn/s/blog_75e063c10100z8vt.html
【14】Opencv中的Adaboost训练源码解读 
http://www.opencvchina.com/thread-129-1-1.html
【15】请研究过cvhaartrainning源码的大牛帮忙~icvLoadTreeCascadeClassifier是什么功能http://www.opencv.org.cn/forum/viewtopic.php?f=10&t=15534
【16】计算haar特征的一个问题,不知大家有没有注意到 
http://www.opencv.org.cn/forum/viewtopic.php?f=1&t=6380
【17】关于haartraining的一些解析，不全 
http://www.opencv.org.cn/forum/viewtopic.php?f=10&t=11129
【18】opencv haartraining 分析二：每级stage正负样本的获取 http://blog.sina.com.cn/s/blog_75e063c10100za53.html
【19】AdaBoost算法程序介绍说明（一）http://blog.sina.com.cn/s/blog_5f853eb10100s9ez.html
【20】AdaBoost算法程序介绍说明（二） http://blog.sina.com.cn/s/blog_5f853eb10100sd65.html
【21】AdaBoost算法程序介绍说明（三） http://blog.sina.com.cn/s/blog_5f853eb10100sdgn.html
【22】 OpenCV 人脸检测自学系列 http://blog.csdn.net/naruto0001/article/details/8029193 （相当不错哦）
【23】基于opencv2.0的haar算法以人脸识别为例的训练分类器xml的方法 http://hi.baidu.com/ccb163163/item/22ba182edcc6fac00e37f9dd
【24】AdaBoost人脸检测训练算法 （上）http://blog.csdn.net/hqw7286/article/details/5556767