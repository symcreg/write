# Qt5.15.2-Opencv4.8.0开发环境搭建
**1. 安装QT5.15.2**  
---
- 进入qt-unified-windows-x64-4.6.0-online.exe所在目录，在文件夹空白处点击右键，选择在终端中打开。
![终端打开](https://www.z4a.net/images/2023/07/18/ed2a295ea19888d71181761936fcc42e.png)
- 使用官方服务器下载及其慢，我们使用腾讯镜像。在终端中输入：
```
.\qt-unified-windows-x64-4.6.0-online.exe --mirror https://mirrors.cloud.tencent.com/qt/
```
![镜像](https://www.z4a.net/images/2023/07/18/2668bc0fb3c8c71320ab7a273818f311.png)
- 回车，选择安装文件夹，在选择组件的步骤，勾选Qt-Qt 5.15.2-MingGw 8.1.0 64-bit，其他保持默认，等待安装完成。
![Qt安装](https://www.z4a.net/images/2023/07/18/02ab9aa7439170c82259be3110c139c3.png)
**2. 解压opencv-4.8.0_build压缩包**
---
- 我们只需关注其中的install文件夹。
![解压](https://www.z4a.net/images/2023/07/18/fc8c9050f79f861ee8cfa4ea0524dd04.png)

**3. 添加环境变量**
---
![环境变量1](https://www.z4a.net/images/2023/07/18/61126fd4fceb69aea62e8936073e651e.png)
![环境变量2](https://www.z4a.net/images/2023/07/18/287bd48793fd191654be98f6b737a635.png)
- 将如下目录添加至环境变量，注意你的路径和我的路径是不同的。
```
C:\Qt\5.15.2\mingw81_64\bin
C:\Qt\Tools\mingw810_64\bin
C:\configure\opencv-4.8.0_build\install\x64\mingw\bin
```
![环境变量3](https://www.z4a.net/images/2023/07/18/6f37459c4f8ac72ba3fcfa0d0706c81e.png)
- **重启电脑使环境变量生效**

**4.测试**
---
- 打开Qt Creator，选择创建项目，如图选择。
![测试1](https://www.z4a.net/images/2023/07/18/6887bab50c677083c0f5b3b6ed68d9b5.png)
![测试2](https://www.z4a.net/images/2023/07/18/2bd385fb80444f78ed471db0baac4e99.png)
![测试3](https://www.z4a.net/images/2023/07/18/51cf54b73fe4438760e6b3d396d0d119.png)
![测试4](https://www.z4a.net/images/2023/07/18/58f575d5688475fc63109564d877b632.png)
![测试5](https://www.z4a.net/images/2023/07/18/5b2ef6fc3545288d46a8fa46153f9187.png)
![测试6](https://www.z4a.net/images/2023/07/18/e2d63f7df31cb759d768aa20b11f4641.png)
- 在pro文件末尾添加下列路径，注意你的路径和我的路径是不同的。
```
INCLUDEPATH += C:\configure\opencv-4.8.0_build\install\include
INCLUDEPATH += C:\configure\opencv-4.8.0_build\install\include\opencv2
LIBS += -L C:\configure\opencv-4.8.0_build\install\x64\mingw\lib\libopencv_*.a
```
![替换1](https://www.z4a.net/images/2023/07/18/imageb8ccf1b07f0c4e1c.png)
- 替换main.cpp文件内容为：
```c++
#include "mainwindow.h"
#include <QApplication>

#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>
#include <opencv2/imgproc/imgproc.hpp>

using namespace cv;

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);

    cv::Mat image = imread("C:\\configure\\1.png");
    namedWindow("Display window",WINDOW_AUTOSIZE);
    imshow("Display window",image);
    waitKey(0);

    MainWindow w;
    w.show();
    return a.exec();
}
```
![替换2](https://www.z4a.net/images/2023/07/18/afdad14e1ea27cc7e1d98f934512e4c8.png)
- 点击左下角的三角形，运行,如果无报错，能显示图片说明一切正常，配置完毕。
![结果](https://www.z4a.net/images/2023/07/18/a58dc9907c156c198cbbcd9d6b1a1e8c.png)
*如想自己编译opencv可参考此链接：[Qt-OpenCV开发环境搭建（史上最详细）](https://blog.csdn.net/Mr_robot_strange/article/details/110677323,"Qt-OpenCV开发环境搭建（史上最详细）")*