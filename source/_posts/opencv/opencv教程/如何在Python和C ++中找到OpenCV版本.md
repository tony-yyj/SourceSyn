---
title: 如何在Python和C ++中输出OpenCV版本号
tags:
  - opencv
  - opencv教程
categories: opencv
abbrlink: 3306323197
date: 2017-09-09 11:30:00
---

<!-- toc -->
<!-- more -->

# 如何在Python中检测OpenCV版本

Python中的一切都很简单。 cv2 .__ version__给你版本字符串。 您可以从中提取主要和次要版本，如下面的示例所示。
```python
import cv2
# Print version string
print "OpenCV version :  {0}".format(cv2.__version__)
 
# Extract major, minor, and subminor version numbers 
(major_ver, minor_ver, subminor_ver) = (cv2.__version__).split('.')
print "Major version :  {0}".format(major_ver)
print "Minor version :  {0}".format(minor_ver)
print "Submior version :  {0}".format(subminor_ver)
 
if int(major_ver) < 3 :
    '''
        Old OpenCV 2 code goes here
    '''
else :
    '''
        New OpenCV 3 code goes here
    '''
```

# 如何在C ++中检测OpenCV版本

在C ++中，几个宏被定义检测到版本 - CV_VERSION，CV_MAJOR_VERSION，CV_MINOR_VERSION，CV_SUBMINOR_VERSION。 以下面的示例代码为例。

```c++
#include "opencv2/opencv.hpp"
 
using namespace cv;
using namespace std;
 
int main( int argc, char** argv )
{
  cout << "OpenCV version : " << CV_VERSION << endl;
  cout << "Major version : " << CV_MAJOR_VERSION << endl;
  cout << "Minor version : " << CV_MINOR_VERSION << endl;
  cout << "Subminor version : " << CV_SUBMINOR_VERSION << endl;
 
  if ( CV_MAJOR_VERSION < 3)
  {
      // Old OpenCV 2 code goes here. 
  } else
  {
      // New OpenCV 3 code goes here. 
  }
}
```

[Blob Detection Using OpenCV ( Python, C++ ) | Learn OpenCV](https://www.learnopencv.com/blob-detection-using-opencv-python-c/)

[How to find OpenCV version in Python and C++ ? | Learn OpenCV](https://www.learnopencv.com/how-to-find-opencv-version-python-cpp/)
