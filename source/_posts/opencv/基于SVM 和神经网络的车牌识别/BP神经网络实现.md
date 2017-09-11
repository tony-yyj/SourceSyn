---
title: BP神经网络的实现
tags:
  - 机器学习
  - opencv项目
categories: opencv
abbrlink: 441658420
date: 2017-09-10 10:30:00
---

<!-- toc -->
<!-- more -->

# 1. 实现BP神经网络

训练一个BP神经网络，实际上就是调整网络的权重和偏置这两个参数。
BP神经网络的训练过程分两部分：
前向传输，逐层波浪式的传递输出值；
逆向反馈，反向逐层调整权重和偏置

# 2. 神经网络的训练过程

1）网络的创建：
1.创建网络（create函数）
2.训练网络（train函数）
3.保存网络（save函数）
2）网络使用
1.读取网络（load函数）
2.实现网络（predict函数）

# 3. 样本数组和样本标记数组

样本数组即为：
```
{{0，0}，{0，1}，{1，0}，{1，1}}
```
而样本标记数组则是每个样本的结果分类，共有4组数据，每组数据的结果都有2种可能，四组数据的输出结果是0，0，0，1，那么，标记样本数组则可以初始化为：
```
 { {1,0}, {1,0}, {1,0}, {0,1} }
```
需要注意的是，两个样本都是由Mat类型储存，且数据类型都定义为 CV_32FC1。

```c++
float labels[4][2] = { {1,0}, {1,0}, {1,0}, {0,1} };
Mat labelsMat(4,2, CV_32FC1, labels);
float trainingData[4][2] = { { 0, 0 }, { 0, 1 }, { 1, 0 }, { 1, 1 } };
Mat trainingDataMat(4, 2, CV_32FC1, trainingData);
```


# 4. 创建神经网络

首先，这组数据的每组输入数据有两组，故输入层的感知器有两个，输出的数组每组也有两个，故输出层感知器个数为2，隐藏层一般情况下都有一到两个，但是在本题中由于不需要隐藏层就可以解决，故无需用到隐藏层，所以该ANN共有两层：输入层（两个感知器）和输出层（两个感知器），（但是按照逻辑来讲，建立隐藏层以后仍旧是可以得到想要的答案的）创建神经网络的函数可以写为：

```c++
CvANN_MLP bp;
Mat layerSizes = (Mat_<int>(1, 2) <<2,2); 
bp.create(layerSizes, CvANN_MLP::SIGMOID_SYM);
```

CvANN_MLP::SIGMOID_SYM ：选用sigmoid作为激励函数，即S形函数（包括单极性S形函数和双极性S形函数）
除此之外，BP所使用的激励函数还有：CvANN_MLP::GAUSSIAN：GAUSS函数,CvANN_MLP::IDENTITY：阶跃函数。

# 5. 训练神经网络

在进行神经网络的训练时，我们就需要用到实现进行初始化好的样本数组和标记数组了，为了方便在图像中显示，我们将样本数组：

```
{{0，0}，{0，1}，{1，0}，{1，1}}
```
进行扩大：
```
{ { 50, 50 }, { 50, 100 }, { 100, 50 }, { 100, 100 } }
```
扩大后直接调用训练函数：

```c++
bp.train(trainingDataMat, labelsMat, Mat(), Mat(), params);
```

关于train函数的参数：

```c++
int CvANN_MLP::train(constMat& inputs, constMat& outputs, 
      constMat& sampleWeights,    constMat& sampleIdx=Mat(), 
      CvANN_MLP_TrainParams params=CvANN_MLP_TrainParams(), intflags=0 );
```

1) inputs：输入矩阵。它存储了所有训练样本的特征。假设所有样本总数为nSamples，而我们提取的特征维数为ndims，
则inputs是一个nSamples∗ndims的矩阵，每个样本的特征占一行。
2) outputs：输出矩阵。我们实际在训练中，我们知道每个样本所属的种类，假设一共有nClass类。那么我们将outputs设置为
一个nSample*nClass列的矩阵，每一行表示一个样本的预期输出结果，该样本所属的那类对应的列设置为1，其他都为0。
比如我们需要识别0-9这10个数字，则总的类数为10类，那么样本数字“3”的预期输出为[0,0,1,0,0,0,0,0,0,0];
3) sampleWeights：一个在使用RPROP方法训练时才需要的数据，如果使用的是BACKPROP方法则不设置，直接设置为Mat()即可。
4) sampleIdx：相当于一个遮罩，它指定哪些行的数据参与训练。如果设置为Mat()，则所有行都参与。
5) params：这个在刚才已经说过了，是训练相关的参数。
其中，params是CvANN_MLP_TrainParams类型的参数，是经过初始化的，训练相关的参数

```c++
 CvANN_MLP_TrainParams params;  
    params.train_method=CvANN_MLP_TrainParams::BACKPROP;  
    params.bp_dw_scale=0.1;  
    params.bp_moment_scale=0.1;  
    //params.train_method=CvANN_MLP_TrainParams::RPROP;  
    //params.rp_dw0 = 0.1;   
    //params.rp_dw_plus = 1.2;   
    //params.rp_dw_minus = 0.5;  
    //params.rp_dw_min = FLT_EPSILON;   
    //params.rp_dw_max = 50.;
```

以上是其初始化参数方法，可以看出，共有两种初始化方法，其中BACKPROP有两个初始化参数，RPROP有五个初始化参数，
BACKPROP表示使用back-propagation的训练方法，
RPROP即最简单的propagation训练方法。Opencv的神经网络实现了MLP算法，具体为BACKPROP算法和RPROP算法两种，BACKPROP算法使用的是在线方法，RPROP算法使用的是批量方法。

在这里我们使用第一种，即BACKPROP方法。

# 6. 保存和加载神经网络

到此神经网络已经搭建完成了，我们可以选择

```c++
bp.save("name.xml");
```

保存神经网络，保存后直接退出或者是继续使用该网络，但是保存后下次使用该神经网络就不必再训练了，只需要使用函数：

```c++
bp.load("name.xml");
```
即可。

# 7. 使用神经网络

图像进行特征提取，把它保存在sampleMat里，通过调用predict函数，我们得到一个输出向量，它是一个1*nClass的行向量，(nClass是可能出现的结果种类数目)

其中每一列说明它与该类的相似程度（0-1之间），也可以说是置信度。我们只用对output求一个最大值，就可得到结果。
这个函数的返回值是一个无用的float值，可以忽略。
在本例子中，由于输入层的感知器数目为2，是图像的坐标，那么，在图像的每一个坐标都去进行分类，得到的是 输出层感知器数目的个数个输出矩阵，每个数代表该种结果的符合率
如：将一个坐标 带入后p[0]==0.1,p[1]==0.5，那么，取拟合率较大的，训练结果是1。


把所有代码总结起来：

```c++
#include <opencv2/core/core.hpp>  
#include <opencv2/highgui/highgui.hpp>  
#include <opencv2/ml/ml.hpp>  
#include <iostream>  
#include <string>  
using namespace std;
using namespace cv;
int main()
{
    CvANN_MLP bp;
    CvANN_MLP_TrainParams params;
    params.train_method = CvANN_MLP_TrainParams::BACKPROP;  
    params.bp_dw_scale = 0.1;
    params.bp_moment_scale = 0.1;
    float labels[4][2] = { {1,0}, {1,0}, {1,0}, {0,1} };
    Mat labelsMat(4,2, CV_32FC1, labels);
    float trainingData[4][2] = { { 50, 50 }, { 50, 100 }, { 100, 50 }, { 100, 100 } };
    Mat trainingDataMat(4, 2, CV_32FC1, trainingData);
    Mat layerSizes = (Mat_<int>(1, 2) <<2,2); 
    bp.create(layerSizes, CvANN_MLP::SIGMOID_SYM);
    bp.train(trainingDataMat, labelsMat, Mat(), Mat(), params);  
    int width = 150, height =150;
    Mat image = Mat::zeros(height, width, CV_8UC3);
    Vec3b green(0, 255, 0), blue(255, 0, 0);
    // Show the decision regions
    for (int i = 0; i < image.rows; ++i){
        for (int j = 0; j < image.cols; ++j){
            Mat sampleMat = (Mat_<float>(1, 2) << i, j);
            Mat responseMat;
            bp.predict(sampleMat, responseMat);
            float* p = responseMat.ptr<float>(0);
            if (p[0] > p[1]){
                image.at<Vec3b>(i,j) = green;
            }
            else{
                image.at<Vec3b>(i,j) = blue;
            }
        }
    }
    int thickness = -1;
    int lineType = 8;
    circle(image, Point(50, 50), 5, Scalar(255, 255, 255), thickness, lineType);
    circle(image, Point(50, 100), 5, Scalar(255, 255, 255), thickness, lineType);
    circle(image, Point(100, 50), 5, Scalar(255, 255, 255), thickness, lineType);
    circle(image, Point(100, 100), 5, Scalar(0,0,0), thickness, lineType);
    imwrite("result.png", image);        // save the image  
    imshow("BP Simple Example", image); // show it to the user  
    waitKey(0);
    return 0;
}
```
[（BP进阶2）学习和实现BP神经网络](http://www.jianshu.com/p/b676d732b982)