## MultiCOMS

### 软件安装

- [Qt环境搭建(Qt Creator)+Visual Studio](http://www.cnblogs.com/ranjiewen/p/5318768.html)
- cn_visual_studio_ultimate_2013_x86_dvd_3009109
- qt-opensource-windows-x86-msvc2013_64_opengl-5.4.1
- qt-vs-addin-1.2.3-opensource

- 按步骤将上面三个文件安装好，既可以在VS下运行Qt工程，首次需要vs配置qt和项目环境，然后运行回报缺少dll文件；然后再将qt的环境变量添加就即可

### 使用方法

- git clone https://github.com/ranjiewwen/QuickLookCameraForCMOS.git

- 使用vs2013打开sln工程设置：
     
     - （1）QT5->Project Setting->Version 选择Qt5.4.1版本
     - （2）QT5->Qt Options->Qt Version->add Qt5.4.1和对应的安装路径
- run即可成功 


**整个软件包含3个主要模块：数据部分、界面显示、相机&显示控制**
- 数据部分：包括网络数据提取，数据处理，数据保存    
 > 通过发指令，硬件开始发送数据，PC端通过UDP接受数据，放入第一级输出缓冲区（process()中完成）；将第一级输出缓冲区和第二级输入缓冲区连接在一起，第二级使用双缓冲，将缓冲区0整帧的数据拷贝到缓冲区1中（process()中完成）；最后通过接口copyArea（）提供给界面显示。对于图像数据保存，彩色图像需要将8位bayer格式数据转为24位RGB数据保存为BMP格式，对于灰度图像，直接保存8位bayer格式数据为BMP格式。
   
   - 界面显示：包括原始采集图像显示，菜单控制相机参数，界面切换   
   >窗口有数据，转换，文件等保护成员，及各种事件处理。菜单栏完成各种控制指令发送，实现对相机和界面的控制，界面切换通过窗口重排实现。
   
   - 控制模块：提供控制接口调整相机参数

### 整个程序流程： 
   - 为每路相机初始化数据处理链路，初始化缓冲区；初始化每路相机数据输入模块(网络，文件)，其输出和数据处理的初级输入端连接起来；为每路相机创建显示界面；为每个界面窗口设置数据，转换，文件；启动所有数据相关的处理流程。主窗口完成初始化，等待窗口事件。


## 附件1：界面显示
 ![image](https://github.com/ranjiewwen/MultiCOMS/blob/master/界面1.png)
 ![image](https://github.com/ranjiewwen/MultiCOMS/blob/master/界面2.png)
## 附件2：保存图像bmp
   ![image](https://github.com/ranjiewwen/MultiCOMS/blob/master/save.bmp)
   ![image](https://github.com/ranjiewwen/MultiCOMS/blob/master/saveToRGB.bmp)
   ![image](https://github.com/ranjiewwen/MultiCOMS/blob/master/other.bmp)
        
##  2015.11--2016.5多CMOS相机上位机——快视系统
- 项目描述：便携式文物鉴定相机

> 
1. 硬件FPGA进行CMOS图像采集，通过网络传输数据，然后在PC上实现4通道CMOS图像显示；
2. 上位机可以通过界面操作完成对相机的控制。

- 项目职责：

> 
1. 制定硬件和PC之间的通信协议；
2. 运用C++编程，通过UDP接收网络数据并提取完整数据帧；
3. 运用Qt编程，使用MVC框架完成图像数据显示，并且完成PC对硬件的控制功能。

## 拓展知识

- 以前没有意识到这其实一个mini的相机系统，实际的成像已经实现
- 当时设置了很多相机参数，其实都是在ISP(图像信号处理)都很常见的参数，也是一些摄影必须了解的知识
- 另外其实显示处理的图像质量，更多的就是图像后处理算法，这些更是相机系统需要做的一些事，例如：去马赛克，去燥，3A算法...
- [ ISP图像处理&&相机系统](https://www.cnblogs.com/ranjiewen/p/9339953.html)

## 日志

- release1 完成基本功能20160310
- release2 完善功能，结项20160620
- update20180721
