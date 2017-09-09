---
title: OpenCV 几个简单示例
tags:
  - opencv
  - opencv教程
categories: opencv
abbrlink: 952441636
date: 2017-09-09 13:00:00
---

<!-- toc -->
<!-- more -->

# 1. OpenCV第一个程序

## 1.1. imread读取图像

```c++
int showPic1()
{
    Mat img = imread("F:\\test.jpg");// 读入一张图片（游戏原画）
    namedWindow("游戏原画");// 创建一个名为 "游戏原画"窗口
    imshow("游戏原画", img);// 在窗口中显示游戏原画
    waitKey(6000);// 等待6000 ms后窗口自动关闭
    return 0;
}
```

## 1.2. cvLoadImage读取图像使用

```c
int showPic2()
{
    const char *pstrImageName = "F:\\test.jpg";
    const char *pstrWindowsTitle = "OpenCV第一个程序";
    //从文件中读取图像
    IplImage *pImage = cvLoadImage(pstrImageName, CV_LOAD_IMAGE_UNCHANGED);
    //创建窗口  
    cvNamedWindow(pstrWindowsTitle, CV_WINDOW_AUTOSIZE);
    //在指定窗口中显示图像  
    cvShowImage(pstrWindowsTitle, pImage);
    //等待按键事件  
    cvWaitKey();
    cvDestroyWindow(pstrWindowsTitle);
    cvReleaseImage(&pImage);
    return 0;
}

```

# 2. 缩放图像

## 2.1. cvCreateImage
函数功能：创建图像
函数原型：
voidcvResize(
  const CvArr* src,
  CvArr* dst,
  intinterpolation=CV_INTER_LINEAR
);

函数说明：

第一个参数表示输入图像

第二个参数表示输出图像。

第三个参数表示插值方法，可以有以下四种：

    CV_INTER_NN - 最近邻插值

    CV_INTER_LINEAR - 双线性插值 (缺省使用)

    CV_INTER_AREA - 使用象素关系重采样。当图像缩小时候，该方法可以避免波纹出现。当图像放大时，类似于 CV_INTER_NN 方法..

    CV_INTER_CUBIC - 立方插值.

完整代码：

```c++
void cvResizePic() {
    const char *pstrImageName = "F:\\test.jpg";
    const char *pstrSaveImageName = "testScale.jpg";
    const char *pstrWindowsSrcTitle = "原图";
    const char *pstrWindowsDstTitle = "缩放图";

    //从文件中读取图像    
    IplImage *pSrcImage = cvLoadImage(pstrImageName, CV_LOAD_IMAGE_UNCHANGED);

    //创建图像并缩放  
    double fScale = 0.314;      //缩放倍数  
    CvSize czSize;              //目标图像尺寸  
    //计算目标图像大小  
    czSize.width = pSrcImage->width * fScale;
    czSize.height = pSrcImage->height * fScale;

    IplImage *pDstImage = NULL;
    pDstImage = cvCreateImage(czSize, pSrcImage->depth, pSrcImage->nChannels);
    cvResize(pSrcImage, pDstImage, CV_INTER_AREA);

    //创建窗口  
    cvNamedWindow(pstrWindowsSrcTitle, CV_WINDOW_AUTOSIZE);
    cvNamedWindow(pstrWindowsDstTitle, CV_WINDOW_AUTOSIZE);

    //在指定窗口中显示图像  
    cvShowImage(pstrWindowsSrcTitle, pSrcImage);
    cvShowImage(pstrWindowsDstTitle, pDstImage);

    //等待按键事件  
    cvWaitKey();

    //保存图片  
    cvSaveImage(pstrSaveImageName, pDstImage);

    cvDestroyWindow(pstrWindowsSrcTitle);
    cvDestroyWindow(pstrWindowsDstTitle);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&pDstImage);
}

```

# 3. Canny边缘检测

[【OpenCV入门指南】第三篇Canny边缘检测](http://blog.csdn.net/morewindows/article/details/8239625)

图像的边缘检测的原理是检测出图像中所有灰度值变化较大的点，而且这些点连接起来就构成了若干线条，这些线条就可以称为图像的边缘。

Canny边缘检测算子是John F. Canny于 1986 年开发出来的一个多级边缘检测算法。

## 3.1. cvCanny函数

功能：采用Canny方法对图像进行边缘检测

原型：

    void cvCanny(

    const CvArr* image,

    CvArr* edges,

    double threshold1,double threshold2,

    int aperture_size=3

    );

函数说明：

第一个参数表示输入图像，必须为**单通道灰度图**。

第二个参数表示输出的边缘图像，为单通道黑白图。

第三个参数和第四个参数表示阈值，这二个阈值中当中的小阈值用来控制边缘连接，大的阈值用来控制强边缘的初始分割即如果一个像素的梯度大与上限值，则被认为是边缘像素，如果小于下限阈值，则被抛弃。如果该点的梯度在两者之间则当这个点与高于上限值的像素点连接时我们才保留，否则删除。

第五个参数表示Sobel 算子大小，默认为3即表示一个3*3的矩阵。Sobel 算子与高斯拉普拉斯算子都是常用的边缘算子

## 3.2. cvCreateTrackbar函数

功能：创建trackbar并添加到指定窗口

## 3.3. CvTrackbarCallback

功能：cvCreateTrackbar()函数所使用的回调函数

```c++
#include <opencv2/opencv.hpp>  
IplImage *g_pSrcImage, *g_pCannyImg;
const char *pstrWindowsCannyTitle = "边缘检测图";
//cvCreateTrackbar的回调函数  
void on_trackbar(int threshold)
{
    //canny边缘检测  
    cvCanny(g_pSrcImage, g_pCannyImg, threshold, threshold * 3, 3);
    cvShowImage(pstrWindowsCannyTitle, g_pCannyImg);
}
int mainCanny()
{
    const char *pstrImageName = "test.jpg";
    const char *pstrWindowsSrcTitle = "原图";
    const char *pstrWindowsToolBar = "Threshold";

    //从文件中载入图像的灰度图CV_LOAD_IMAGE_GRAYSCALE - 灰度图  
    g_pSrcImage = cvLoadImage(pstrImageName, CV_LOAD_IMAGE_GRAYSCALE);
    g_pCannyImg = cvCreateImage(cvGetSize(g_pSrcImage), IPL_DEPTH_8U, 1);

    //创建窗口  
    cvNamedWindow(pstrWindowsSrcTitle, CV_WINDOW_AUTOSIZE);
    cvNamedWindow(pstrWindowsCannyTitle, CV_WINDOW_AUTOSIZE);

    //创建滑动条  
    int nThresholdEdge = 10;
    cvCreateTrackbar(pstrWindowsToolBar, pstrWindowsCannyTitle, &nThresholdEdge, 150, on_trackbar);

    //在指定窗口中显示图像  
    cvShowImage(pstrWindowsSrcTitle, g_pSrcImage);
    on_trackbar(nThresholdEdge);

    //等待按键事件  
    cvWaitKey();

    cvDestroyWindow(pstrWindowsSrcTitle);
    cvDestroyWindow(pstrWindowsCannyTitle);
    cvReleaseImage(&g_pSrcImage);
    cvReleaseImage(&g_pCannyImg);
    return 0;
}

```

# 4. 图像的二值化

[【OpenCV入门指南】第四篇 图像的二值化 morewindows](http://blog.csdn.net/morewindows/article/details/8239678)

- 与边缘检测相比，轮廓检测有时能更好的反映图像的内容。而要对图像进行轮廓检测，则必须要先对图像进行二值化.
- 图像的二值化就是将图像上的像素点的灰度值设置为0或255，这样将使整个图像呈现出明显的黑白效果。图像的二值化使图像中数据量大为减少，从而能凸显出目标的轮廓。

## 4.1. 二值化函数cvThreshold()。

函数功能：采用Canny方法对图像进行边缘检测

- OpenCV还有个cvAdaptiveThreshold()函数，这个函数会使用Otsu算法(大律法或最大类间方差法)来计算出一个全局阈值，然后根据这个阈值进行二值化。

- 调用cvThreshold()时传入参数CV_THRESH_OTSU也是使用Otsu算法来自动生成一个阈值。

- 当然直接使用Canny边缘检测中的cvCanny()函数也可以对图像进行二值化

```c++
//图像的二值化   cvThreshold
//图像的二值化就是将图像上的像素点的灰度值设置为0或255，
//这样将使整个图像呈现出明显的黑白效果。
//By MoreWindows http://blog.csdn.net/morewindows/article/details/8239678
#include <opencv2/opencv.hpp>  
IplImage *g_pGrayImage = NULL;
IplImage *g_pBinaryImage = NULL;
const char *pstrWindowsBinaryTitle = "二值图)";

void on_trackbarB(int pos)
{
    // 转为二值图  
    cvThreshold(g_pGrayImage, g_pBinaryImage, pos, 255, CV_THRESH_BINARY);
    // 显示二值图  
    cvShowImage(pstrWindowsBinaryTitle, g_pBinaryImage);
}

int mainBinary()
{
    const char *pstrWindowsSrcTitle = "原图";
    const char *pstrWindowsToolBarName = "二值图阈值";

    // 从文件中加载原图  
    IplImage *pSrcImage = cvLoadImage("test.jpg", CV_LOAD_IMAGE_UNCHANGED);

    // 转为灰度图  
    g_pGrayImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);
    cvCvtColor(pSrcImage, g_pGrayImage, CV_BGR2GRAY);

    // 创建二值图  
    g_pBinaryImage = cvCreateImage(cvGetSize(g_pGrayImage), IPL_DEPTH_8U, 1);

    // 显示原图  
    cvNamedWindow(pstrWindowsSrcTitle, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsSrcTitle, pSrcImage);
    // 创建二值图窗口  
    cvNamedWindow(pstrWindowsBinaryTitle, CV_WINDOW_AUTOSIZE);

    // 滑动条    
    int nThreshold =100;
    cvCreateTrackbar(pstrWindowsToolBarName, pstrWindowsBinaryTitle,
        &nThreshold, 254, on_trackbarB);
    on_trackbarB(nThreshold);

    cvWaitKey(0);
    cvDestroyWindow(pstrWindowsSrcTitle);
    cvDestroyWindow(pstrWindowsBinaryTitle);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&g_pGrayImage);
    cvReleaseImage(&g_pBinaryImage);
    return 0;
}

```

# 5. 轮廓检测

[【OpenCV入门指南】第五篇 轮廓检测 上 - MoreWindows Blog](http://blog.csdn.net/morewindows/article/details/8253137)

轮廓检测的原理通俗的说就是掏空内部点，比如原图中有3 * 3的矩形点。那么就可以将中间的那一点去掉

## 5.1. 函数cvFindContours cvDrawContours

- cvFindContours函数功能：对图像进行轮廓检测，这个函数将生成一条链表以保存检测出的各个轮廓信息，并传出指向这条链表表头的指针。
- cvDrawContours函数功能：在图像上绘制外部和内部轮廓

```c++
#include <opencv2/opencv.hpp>  
int mainContours()
{
    const char *pstrWindowsSrcTitle = "原图";
    const char *pstrWindowsOutLineTitle = "轮廓图";
    
    //1. 创建图像  
    const int IMAGE_WIDTH = 400;
    const int IMAGE_HEIGHT = 200;
    IplImage *pSrcImage = cvCreateImage(cvSize(IMAGE_WIDTH, IMAGE_HEIGHT), IPL_DEPTH_8U, 3);
    // 填充成白色  
    cvRectangle(pSrcImage, cvPoint(0, 0), cvPoint(pSrcImage->width, pSrcImage->height), CV_RGB(255, 255, 255), CV_FILLED);
    // 画圆  
    CvPoint ptCircleCenter = cvPoint(IMAGE_WIDTH / 4, IMAGE_HEIGHT / 2);
    int nRadius = 80;
    cvCircle(pSrcImage, ptCircleCenter, nRadius, CV_RGB(255, 255, 0), CV_FILLED);
    ptCircleCenter = cvPoint(IMAGE_WIDTH / 4, IMAGE_HEIGHT / 2);
    nRadius = 30;
    cvCircle(pSrcImage, ptCircleCenter, nRadius, CV_RGB(255, 255, 255), CV_FILLED);
    // 画矩形  
    CvPoint ptLeftTop = cvPoint(IMAGE_WIDTH / 2 + 20, 20);
    CvPoint ptRightBottom = cvPoint(IMAGE_WIDTH - 20, IMAGE_HEIGHT - 20);
    cvRectangle(pSrcImage, ptLeftTop, ptRightBottom, CV_RGB(0, 255, 255), CV_FILLED);
    ptLeftTop = cvPoint(IMAGE_WIDTH / 2 + 60, 40);
    ptRightBottom = cvPoint(IMAGE_WIDTH - 60, IMAGE_HEIGHT - 40);
    cvRectangle(pSrcImage, ptLeftTop, ptRightBottom, CV_RGB(255, 255, 255), CV_FILLED);
    // 显示原图  
    cvNamedWindow(pstrWindowsSrcTitle, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsSrcTitle, pSrcImage);

    //2. 转为灰度图  
    IplImage *pGrayImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);
    cvCvtColor(pSrcImage, pGrayImage, CV_BGR2GRAY);
    // 转为二值图  
    IplImage *pBinaryImage = cvCreateImage(cvGetSize(pGrayImage), IPL_DEPTH_8U, 1);
    cvThreshold(pGrayImage, pBinaryImage, 250, 255, CV_THRESH_BINARY);


    //3. 检索轮廓并返回检测到的轮廓的个数  
    CvMemStorage *pcvMStorage = cvCreateMemStorage();
    CvSeq *pcvSeq = NULL;
    cvFindContours(pBinaryImage, pcvMStorage, &pcvSeq, sizeof(CvContour), CV_RETR_TREE, CV_CHAIN_APPROX_SIMPLE, cvPoint(0, 0));

    //4. 画轮廓图  
    IplImage *pOutlineImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 3);
    int nLevels = 5;
    // 填充成白色  
    cvRectangle(pOutlineImage, cvPoint(0, 0), cvPoint(pOutlineImage->width, pOutlineImage->height), CV_RGB(255, 255, 255), CV_FILLED);
    cvDrawContours(pOutlineImage, pcvSeq, CV_RGB(255, 0, 0), CV_RGB(0, 255, 0), nLevels, 2);
    // 显示轮廓图  
    cvNamedWindow(pstrWindowsOutLineTitle, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsOutLineTitle, pOutlineImage);
    cvWaitKey(0);
    cvReleaseMemStorage(&pcvMStorage);
    cvDestroyWindow(pstrWindowsSrcTitle);
    cvDestroyWindow(pstrWindowsOutLineTitle);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&pGrayImage);
    cvReleaseImage(&pBinaryImage);
    cvReleaseImage(&pOutlineImage);
    return 0;
}
```


实例:
[【OpenCV入门指南】第六篇 轮廓检测 下 - MoreWindows Blog](http://blog.csdn.net/morewindows/article/details/8253174)

```c++
//图像的轮廓检测下  
//http://blog.csdn.net/morewindows/article/details/8253174
#include <opencv2/opencv.hpp>  

IplImage *g_pGrayImage2 = NULL;
const char *pstrWindowsBinaryTitle2 = "二值图";
const char *pstrWindowsOutLineTitle = "轮廓图";
CvSeq *g_pcvSeq = NULL;

void on_trackbarC(int pos)
{
    // 转为二值图  
    IplImage *pBinaryImage = cvCreateImage(cvGetSize(g_pGrayImage2), IPL_DEPTH_8U, 1);
    cvThreshold(g_pGrayImage2, pBinaryImage, pos, 255, CV_THRESH_BINARY);
    // 显示二值图  
    cvShowImage(pstrWindowsBinaryTitle2, pBinaryImage);

    //找轮廓
    CvMemStorage* cvMStorage = cvCreateMemStorage();
    // 检索轮廓并返回检测到的轮廓的个数  
    cvFindContours(pBinaryImage, cvMStorage, &g_pcvSeq);

    //绘制轮廓
    IplImage *pOutlineImage = cvCreateImage(cvGetSize(g_pGrayImage2), IPL_DEPTH_8U, 3);
    int _levels = 5;
    cvZero(pOutlineImage);//初始化图片，值都为0
    cvDrawContours(pOutlineImage, g_pcvSeq, CV_RGB(255, 0, 0), CV_RGB(0, 255, 0), _levels);
    cvShowImage(pstrWindowsOutLineTitle, pOutlineImage);

    cvReleaseMemStorage(&cvMStorage);
    cvReleaseImage(&pBinaryImage);
    cvReleaseImage(&pOutlineImage);
}

int mainFindContours()
{
    const char *pstrWindowsSrcTitle = "原图";
    const char *pstrWindowsToolBarName = "二值化";

    // 从文件中加载原图  
    const char *pstrImageName = "test.jpg";
    IplImage *pSrcImage = cvLoadImage(pstrImageName, CV_LOAD_IMAGE_UNCHANGED);
    // 显示原图  
    cvNamedWindow(pstrWindowsSrcTitle, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsSrcTitle, pSrcImage);

    // 转为灰度图  
    g_pGrayImage2 = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);
    cvCvtColor(pSrcImage, g_pGrayImage2, CV_BGR2GRAY);

    // 创建二值图和轮廓图窗口  
    cvNamedWindow(pstrWindowsBinaryTitle2, CV_WINDOW_AUTOSIZE);
    cvNamedWindow(pstrWindowsOutLineTitle, CV_WINDOW_AUTOSIZE);


    // 滑动条    
    int nThreshold = 80;
    cvCreateTrackbar(pstrWindowsToolBarName, pstrWindowsBinaryTitle2, &nThreshold, 254, on_trackbarC);

    on_trackbarC(nThreshold);

    cvWaitKey(0);
    cvDestroyWindow(pstrWindowsSrcTitle);
    cvDestroyWindow(pstrWindowsBinaryTitle2);
    cvDestroyWindow(pstrWindowsOutLineTitle);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&g_pGrayImage2);
    return 0;
}
```

# 6. 线段检测与圆检测

[【OpenCV入门指南】第七篇 线段检测与圆检测 - MoreWindows Blog](http://blog.csdn.net/morewindows/article/details/8266985)
线段检测与圆检测主要运用Hough变换，Hough变换是一种利用图像的全局特征将特定形状的边缘连接起来，形成连续平滑边缘的一种方法。它通过将源图像上的点影射到用于累加的参数空间，实现对已知解析式曲线进行识别。

## 6.1. 函数cvHoughLines2和cvHoughCircles

线段检测和圆检测已经封装成函数了，直接使用cvHoughLines2和cvHoughCircles即可，下面来看看函数介绍和实际代码。

```c++

#include <opencv2/opencv.hpp>  
int mainHoughLines()
{
    const char *pstrWindowsSrcTitle = "原图(http://blog.csdn.net/MoreWindows)";
    const char *pstrWindowsLineName = "线段检测";

    // 从文件中加载原图  
    IplImage *pSrcImage = cvLoadImage("testCircle.jpg", CV_LOAD_IMAGE_UNCHANGED);
    // 灰度图  
    IplImage *pGrayImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);
    cvCvtColor(pSrcImage, pGrayImage, CV_BGR2GRAY);
    // 边缘图  
    IplImage *pCannyImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);
    cvCanny(pGrayImage, pCannyImage, 30, 90);
    //cvSmooth(pCannyImage, pCannyImage);  

    // 线段检测(只能针对二值图像)  
    CvMemStorage *pcvMStorage = cvCreateMemStorage();
    double fRho = 1;//第四个参数表示与象素相关单位的距离精度。
    double fTheta = CV_PI / 180;//第五个参数表示弧度测量的角度精度。
    int nMaxLineNumber = 50;   //最多检测条直线  
    double fMinLineLen = 50;   //最小线段长度  
    double fMinLineGap = 10;   //最小线段间隔  
    CvSeq *pcvSeqLines = cvHoughLines2(pCannyImage, pcvMStorage, CV_HOUGH_PROBABILISTIC,
        fRho, fTheta, nMaxLineNumber, fMinLineLen, fMinLineGap);

    // 绘制线段  
    IplImage *pColorImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 3);
    cvCvtColor(pCannyImage, pColorImage, CV_GRAY2BGR);
    int i;
    for (i = 0; i < pcvSeqLines->total; i++)
    {
        CvPoint* line = (CvPoint*)cvGetSeqElem(pcvSeqLines, i);
        cvLine(pColorImage, line[0], line[1], CV_RGB(255, 0, 0), 2);
    }

    cvNamedWindow(pstrWindowsSrcTitle, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsSrcTitle, pSrcImage);
    cvNamedWindow(pstrWindowsLineName, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsLineName, pColorImage);

    cvWaitKey(0);
    cvReleaseMemStorage(&pcvMStorage);
    cvDestroyWindow(pstrWindowsSrcTitle);
    cvDestroyWindow(pstrWindowsLineName);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&pGrayImage);
    cvReleaseImage(&pCannyImage);
    cvReleaseImage(&pColorImage);
    return 0;
}

int mainHoughCircles()
{
    const char *pstrWindowsSrcTitle = "原图";
    const char *pstrWindowsLineName = "圆检测";

    // 从文件中加载原图  
    IplImage *pSrcImage = cvLoadImage("testCircle.jpg", CV_LOAD_IMAGE_UNCHANGED);
    // 灰度图  
    IplImage *pGrayImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);
    cvCvtColor(pSrcImage, pGrayImage, CV_BGR2GRAY);
    //cvSmooth(pGrayImage, pGrayImage);  

    // 圆检测(灰度图)  
    CvMemStorage *pcvMStorage = cvCreateMemStorage();
    double fMinCircleGap = pGrayImage->height / 10;
    //第三个参数表示寻找圆弧圆心的累计分辨率，通常设置成1就可以了。这里设置为2可见
    CvSeq *pcvSeqCircles = cvHoughCircles(pGrayImage, pcvMStorage, CV_HOUGH_GRADIENT,
        2, fMinCircleGap);
    //每个圆由三个浮点数表示：圆心坐标(x,y)和半径  

    // 绘制直线  
    IplImage *pColorImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 3);
    cvCvtColor(pGrayImage, pColorImage, CV_GRAY2BGR);
    int i;
    for (i = 0; i < pcvSeqCircles->total; i++)
    {
        float* p = (float*)cvGetSeqElem(pcvSeqCircles, i);
        cvCircle(pColorImage, cvPoint(cvRound(p[0]), cvRound(p[1])), cvRound(p[2]), CV_RGB(255, 0, 0), 2);
    }

    cvNamedWindow(pstrWindowsSrcTitle, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsSrcTitle, pSrcImage);
    cvNamedWindow(pstrWindowsLineName, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsLineName, pColorImage);

    cvWaitKey(0);
    cvReleaseMemStorage(&pcvMStorage);
    cvDestroyWindow(pstrWindowsSrcTitle);
    cvDestroyWindow(pstrWindowsLineName);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&pGrayImage);
    cvReleaseImage(&pColorImage);
    return 0;
}
```

# 7. 灰度直方图均衡化

绍直方图的均衡化，这是图像增强的常用方法。下面来看看灰度直方图均衡化的

## 7.1. 函数cvEqualizeHist

```c++
//图像的灰度直方图  
//http://blog.csdn.net/morewindows/article/details/8364656
#include <opencv2/opencv.hpp>
//#include <opencv2/legacy/compat.hpp>
#define cvQueryHistValue_1D( hist, idx0 ) \
    ((float)cvGetReal1D( (hist)->bins, (idx0)))

void FillWhite(IplImage *pImage)
{
    cvRectangle(pImage, cvPoint(0, 0), cvPoint(pImage->width, pImage->height), CV_RGB(255, 255, 255), CV_FILLED);
}
// 创建灰度图像的直方图
CvHistogram* CreateGrayImageHist(IplImage **ppImage)
{
    int nHistSize = 256;
    float fRange[] = { 0, 255 };  //灰度级的范围
    float *pfRanges[] = { fRange };
    //cvCreateHist 创建直方图    CvHistogram直方图的数据结构
    int dims = 1;//直方图维数，灰度图为1，彩色图为3
    CvHistogram *pcvHistogram = cvCreateHist(dims, &nHistSize, CV_HIST_ARRAY, pfRanges);
    //cvCalcHist根据图像计算直方图
    cvCalcHist(ppImage, pcvHistogram);
    return pcvHistogram;
}
// 根据直方图创建直方图图像
IplImage* CreateHisogramImage(int nImageWidth, int nScale, int nImageHeight, CvHistogram *pcvHistogram)
{
    IplImage *pHistImage = cvCreateImage(cvSize(nImageWidth * nScale, nImageHeight), IPL_DEPTH_8U, 1);
    FillWhite(pHistImage);

    //统计直方图中的最大直方块
    float fMaxHistValue = 0;
    cvGetMinMaxHistValue(pcvHistogram, NULL, &fMaxHistValue, NULL, NULL);

    //分别将每个直方块的值绘制到图中
    int i;
    for (i = 0; i < nImageWidth; i++)
    {
        float fHistValue = cvQueryHistValue_1D(pcvHistogram, i); //像素为i的直方块大小
        int nRealHeight = cvRound((fHistValue / fMaxHistValue) * nImageHeight);  //要绘制的高度
        cvRectangle(pHistImage,
            cvPoint(i * nScale, nImageHeight - 1),
            cvPoint((i + 1) * nScale - 1, nImageHeight - nRealHeight),
            cvScalar(i, 0, 0, 0),
            CV_FILLED
            );
    }
    return pHistImage;
}

int mainHist()
{
    const char *pstrWindowsSrcTitle = "原图";
    const char *pstrWindowsGrayTitle = "灰度图";
    const char *pstrWindowsHistTitle = "直方图";
    const char *pstrWindowsGrayEqualizeTitle = "灰度图-均衡化后";
    const char *pstrWindowsHistEqualizeTitle = "直方图-均衡化后";

    //1.从文件中加载原图
    IplImage *pSrcImage = cvLoadImage("Unequalized_Hawkes_Bay_NZ.jpg", CV_LOAD_IMAGE_UNCHANGED);
    IplImage *pGrayImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);
    IplImage *pGrayEqualizeImage = cvCreateImage(cvGetSize(pSrcImage), IPL_DEPTH_8U, 1);

    // 灰度图
    cvCvtColor(pSrcImage, pGrayImage, CV_BGR2GRAY);

    //2.灰度直方图及直方图图像  
    CvHistogram *pcvHistogram = CreateGrayImageHist(&pGrayImage);

    // 直方图图像数据  
    int nHistImageWidth = 255;
    int nHistImageHeight = 150;
    int nScale = 2;
    IplImage *pHistImage = CreateHisogramImage(nHistImageWidth, nScale, 
        nHistImageHeight, pcvHistogram);

    // 均衡化  cvEqualizeHist 图像增强的常用方法
    //函数功能：直方图均衡化，该函数能归一化图像亮度和增强对比度
    //第一个参数表示输入图像，必须为灰度图（8位，单通道图）
    //第二个参数表示输出图像
    //该函数采用如下法则对输入图像进行直方图均衡化：
    //1：计算输入图像的直方图H。
    //2：直方图归一化，因此直方块和为255。
    //3：计算直方图积分，H‘(i) = Sum(H(j)) (0<=j<=i)。
    //4：采用H‘作为查询表：dst(x, y) = H‘(src(x, y))进行图像变换。
    cvEqualizeHist(pGrayImage, pGrayEqualizeImage);

    // 均衡化后的灰度直方图及直方图图像  
    CvHistogram *pcvHistogramEqualize = CreateGrayImageHist(&pGrayEqualizeImage);
    IplImage *pHistEqualizeImage = CreateHisogramImage(nHistImageWidth, nScale, nHistImageHeight, pcvHistogramEqualize);

    // 显示
    cvNamedWindow(pstrWindowsSrcTitle, CV_WINDOW_AUTOSIZE);
    //cvNamedWindow(pstrWindowsGrayTitle, CV_WINDOW_AUTOSIZE);
    cvNamedWindow(pstrWindowsHistTitle, CV_WINDOW_AUTOSIZE);
    cvNamedWindow(pstrWindowsGrayEqualizeTitle, CV_WINDOW_AUTOSIZE);
    cvNamedWindow(pstrWindowsHistEqualizeTitle, CV_WINDOW_AUTOSIZE);
    cvShowImage(pstrWindowsSrcTitle, pSrcImage);
    //cvShowImage(pstrWindowsGrayTitle, pGrayImage);
    cvShowImage(pstrWindowsHistTitle, pHistImage);
    cvShowImage(pstrWindowsGrayEqualizeTitle, pGrayEqualizeImage);
    cvShowImage(pstrWindowsHistEqualizeTitle, pHistEqualizeImage);

    cvWaitKey(0);
    cvReleaseHist(&pcvHistogram);
    cvDestroyWindow(pstrWindowsSrcTitle);
    cvDestroyWindow(pstrWindowsGrayTitle);
    cvDestroyWindow(pstrWindowsHistTitle);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&pGrayImage);
    cvReleaseImage(&pHistImage);
    return 0;
}
```

# 8. 彩色直方图均衡化

[【OpenCV入门指南】第十篇 彩色直方图均衡化 - MoreWindows Blog](http://blog.csdn.net/morewindows/article/details/8364722)

在OpenCV中，彩色的图像其实是用一个多通道数组来存储的，每个单通道数组中的元素的取值范围都是0到255。这与灰度图中像素的变化范围是相同的。因此对彩色图像进行直方图均衡化只要先将彩色图像分解成若干通道，然后这些通道分别进行直方图均衡化，最后合并所有通道即可。下面介绍下二个主要函数cvSplit()和cvMerge()。

## 8.1. cvSplit()和cvMerge()

```c++
//图像的增强  彩色直方图均衡化
#include <opencv2/opencv.hpp>
using namespace std;
IplImage* EqualizeHistColorImage(IplImage *pImage)
{
    // 原图像分成各通道后再均衡化,最后合并即彩色图像的直方图均衡化  
    const int MAX_CHANNEL = 4;
    IplImage *pImageChannel[MAX_CHANNEL] = { NULL };
    int i;
    for (i = 0; i < pImage->nChannels; i++)
    {
        pImageChannel[i] = cvCreateImage(cvGetSize(pImage), pImage->depth, 1);
    }
    cvSplit(pImage, pImageChannel[0], pImageChannel[1], pImageChannel[2], pImageChannel[3]);

    for (  i = 0; i < pImage->nChannels; i++)
    {
        cvEqualizeHist(pImageChannel[i], pImageChannel[i]);
    }
    IplImage *pEquaImage = cvCreateImage(cvGetSize(pImage), pImage->depth, 3);
    cvMerge(pImageChannel[0], pImageChannel[1], pImageChannel[2], pImageChannel[3], pEquaImage);

    return pEquaImage;

}

int EqualizeHistColorMain(const char *filename) 
{
    const char *pstrWindowSrcTitle = "原图";
    const char *pstrWindowHistEquaTitle = "均衡化后";
    cvNamedWindow(pstrWindowSrcTitle, CV_WINDOW_AUTOSIZE);
    cvNamedWindow(pstrWindowHistEquaTitle, CV_WINDOW_AUTOSIZE);

    IplImage *pSrcImage = cvLoadImage(filename, CV_LOAD_IMAGE_UNCHANGED);
    IplImage *pHistEquaImage = EqualizeHistColorImage(pSrcImage);

    cvShowImage(pstrWindowSrcTitle, pSrcImage);
    cvShowImage(pstrWindowHistEquaTitle, pHistEquaImage);
    cvWaitKey(0);
    cvDestroyWindow(pstrWindowSrcTitle);
    cvDestroyWindow(pstrWindowHistEquaTitle);
    cvReleaseImage(&pSrcImage);
    cvReleaseImage(&pHistEquaImage);
    return 0;
}
```
