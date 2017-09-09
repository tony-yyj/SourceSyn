---
title: OpenCV 第一个程序Hello World
tags:
  - opencv
  - opencv教程
categories: opencv
abbrlink: 3210282281
date: 2017-09-09 13:30:00
---

<!-- toc -->
<!-- more -->

# 屏幕上显示一幅图像

第一种方式

```c++
//C++输入输出库头文件
#include <iostream>
//OpenCV核心库头文件
#include <opencv2\core\core.hpp>
//OpenCV图形处理头文件
#include <opencv2\highgui\highgui.hpp>

//OpenCV核心动态链接库，和core.hpp头文件对应，d代表调试版本
#pragma comment(lib,"opencv_core242d.lib")
//OpenCV图形处理动态链接库，和highgui.hpp头文件对应，d代表调试版本
#pragma comment(lib,"opencv_highgui242d.lib")

int main(int argc, _TCHAR* argv[])
{
    // 窗口名称
    std::string windowName = "HelloWorld";
    //图像名称
    std::string imgFile = "opencv-logo.png";
    //读入图像
    cv::Mat image = cv::imread(imgFile,CV_LOAD_IMAGE_COLOR);
    //如果无法读取图形
    if(!image.data)
    {
        std::cout << "无法打开图像文件" <<std::endl;
        system("PAUSE");//暂停窗口
        return -1;
    }
    //创建一个新窗口
    cv::namedWindow(windowName,CV_WINDOW_AUTOSIZE);
    //将图像显示都新创建的窗口中
    cv::imshow(windowName,image);
    //等待，直到用户按任意键时退出
    cv::waitKey(0);

    return 0;
}
```

第二种方式
```c++
#include "highgui.h"

int main( int argc, char** argv )
{

    // cvLoadImage可以读取大多数格式的图像文件，BMP、DIB、JPEG、JPE、PNG、BBM、PPM  SR、RAS、TIFF  
    // 函数执行完后返回一个指针，此指针指向一块为描述该图像文件的数据结构而分配的内存块。
    IplImage* img = cvLoadImage( argv[1] );

    // cvNamedWindow由HighGUI库提供，用于在屏幕上创建一个窗口，将被显示的图像包含于该窗口中。  
    // 函数第一个参数指定了窗口的的窗口标题。
    cvNamedWindow("HelloWorld", CV_WINDOW_AUTOSIZE );

    // 显示该图像
    cvShowImage("HelloWorld", img );

    // 使程序暂停，等待用户触发一个按键操作，但如果该函数参数设为一个正数，则程序将暂停一段时间
    cvWaitKey(0);
    cvReleaseImage( &img ); // 内存释放功能
    cvDestroyWindow("HelloWorld");  
}  
```

# 播放AVI视频

```c++
#include "highgui.h"

int main( int argc, char** argv ) { 
    cvNamedWindow( "Example2", CV_WINDOW_AUTOSIZE );
	// cvCaptureFromAVI()通过参数设置要读入的AVI文件，返回一个指向cvCapture结构的指针
	// 这个指针包括了所有关于读入AVI文件的信息，其中包括状态信息。
	// 在调用这个函数后，返回指针指向的CvCapture结构被初始化到所对应的AVI文件的开头。
    //CvCapture* capture = cvCaptureFromAVI( argv[1] ); // either one will work
    CvCapture* capture = cvCreateFileCapture( argv[1] );
    IplImage* frame;
    while(1) {
		// 用来将下一帧视频文件载入内存（实际上是填充或更新CvCapture结构中），返回一个
		// 对应当前帧的指针
		// 与cvLoadImage不同的是，cvLoadImage为图像分配内存空间，而cvQueryFram使用已经在
		// cvCapture结构中分配好的内存，这样的话没必要通过cvReleaseImage()对返回值释放。
        frame = cvQueryFrame( capture );
        if( !frame ) break;
        cvShowImage( "Example2", frame );
        char c = cvWaitKey(33);
        if( c == 27 ) break;
    }
    cvReleaseCapture( &capture );
    cvDestroyWindow( "Example2" );
}
```