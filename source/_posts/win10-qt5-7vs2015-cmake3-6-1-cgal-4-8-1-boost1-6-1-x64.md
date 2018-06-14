---
title: win10+QT5.7+vs2015+CMake3.6.1+cgal-4.8.1+boost1.6.1 64位开发环境配置
tags:
  - boost
  - cgal
  - cmake
  - qt5
  - vs2010
  - opengl
id: 346
categories:
  - CG
date: 2016-08-19 10:06:39
---

有一个项目，原来是在win7 64位 QT4.8.5上开发的,原来用的是cgal-4.2 boost-1.5.4。现移植到win10 64位 vs2015 QT5.7上 cgal-4.8.1 boost1.6.1上开发。

### 一、安装win10。

我的是win10教育版，64位。

### 二、安装vs2015。

我的是vs2015专业版。

### 三、安装QT5.7。

我是安装的64位，到QT官网上下载的qt-opensource-windows-x86-msvc2015_64-5.7.0.exe， 下载地址[https://www.qt.io/download-open-source/#section-2](https://www.qt.io/download-open-source/#section-2)。

然后到微软的网站上下载了一个Qt5Package.vsix文件，下载地址：[https://visualstudiogallery.msdn.microsoft.com/c89ff880-8509-47a4-a262-e4fa07168408](https://visualstudiogallery.msdn.microsoft.com/c89ff880-8509-47a4-a262-e4fa07168408)，安装之后，在vs2015中才会有一个QT5菜项。据说vs2015中Visual Studio Add-in 1.2.5 for Qt5不能使用了，没试过。

安装Qt5Package.vsix后，vs2015中会有一个菜单QT5，有一个菜单荐Qt Options，点开可以add，QT的版本好和路径，也有一个QT Project Settings菜单项，可以改变或设置项目的QT版本号。

我配置了环境变量QTDIR，指向了C:\Qt\Qt5.7.0\5.7\msvc2015_64，并且把C:\Qt\Qt5.7.0\5.7\msvc2015_64\bin添加到了path路径中。

### 四、配置boost

boost官网是[http://www.boost.org/](http://www.boost.org/)，可以从官网上找到链接跳到[https://sourceforge.net/projects/boost/files/boost/1.61.0/](https://sourceforge.net/projects/boost/files/boost/1.61.0/)进行下载，我下载的是boost_1_61_0.7z。

我下载后解压boost_1_61_0.7z，到目录D:\geometry_lib\boost_1_61_0，里面有一个bootstrap.bat 文件。

我以管理员权限启动命令行cmd，进入到D:\geometry_lib\boost_1_61_0。直接运行bootstrap.bat。然后D:\geometry_lib\boost_1_61_0目录中，会生成b2.exe和bjam.exe， 如果直接运行b2.exe或者bjam.exe会生成根据操作系统上默认的编译器编译出boost的相关的库，应该是32位的吧。

而我需要64位的，用于vs2015的，我就在命令行中接着运行bjam.exe address-model=64,其中 address-model=64保证编译的是64位的库。如果要指定编译器，比如系统上同时安装有vs2012和vs2015，想用vs2012编译库，可运行bjam.exe --toolset=msvc-11.0，如果需要编译64位的话，运行bjam.exe --toolset=msvc-12.0 address-model=64。其中参数--toolset=msvc-11.0指定使用vs2012对应的编译器，vs2013是msvc-12.0，vs2015是msvc-14.0 。

这样就编译好了，为生成stage/lib目录，lib目录中就是编译好的库。

**配置环境变量** 添加环境变量BOOST_ROOT，指向bootstrap.bat所在的目录，我的为D:\geometry_lib\boost_1_61_0。添加环境变量BOOST_LIBRARYDIR，我的为D:\geometry_lib\boost_1_61_0\stage\lib。

### 五、配置CGAL

CGAL的官网站是[http://www.cgal.org/download/windows.html](http://www.cgal.org/download/windows.html)，其中有链接跳转到[https://github.com/CGAL/cgal/releases](https://github.com/CGAL/cgal/releases)，进行下载，我下载的是CGAL-4.8-Setup.exe文件，双击会让选择32bit还是64bit，我要64位的所以选择了64bit的进行安装(实际上是解压)，我使用它的默认解压路径，解压到了C:\dev\CGAL-4.8.1。

打开CMAKE，“Where is the source code:”栏目填CGAL的解压路径，我的是C:\dev\CGAL-4.8.1。"Where to build the binaries"栏目填要把build库等文件放在个目录，我填的是C:\dev\CGAL-4.8.1\build。然后，点Configure按钮，我没遇到错误，会弹出编译器选择话框，我选的是vs2015 64位的，好像对应的是msvc 14 win64之类的，然后点Generate，会在C:\dev\CGAL-4.8.1\build目录下生成CGAL.sln文件。我双击用vs2015打开CGAL.sln，分别在Debug和Release模式下，点“生成”菜单下的“生成解决方案”，编译出对应的库(C:\dev\CGAL-4.8.1\build\lib目录下，其中带gd的lib文件是debug版的).

使用时，在需要CGAL的项目上右键-》属性-》VC++目录： 包含目录加入: CGAL安装路径\include;CGAL安装路径\auxiliary\gmp\include;Boost安装路径;CGAL编译输出路径\include

库目录加入: CGAL输出目录\lib;CGAL安装路径\auxiliary\gmp\lib;Boost安装路径\stage\lib 我的项目中添加链接器-->输入-->附加依赖型：qtmain.lib Qt5Core.lib Qt5Gui.lib Qt5Widgets.lib Qt5OpenGL.lib opengl32.lib glu32.lib libgmp-10.lib libmpfr-4.lib

理论上，可以使用CGAL了。

但我使用时，报一些错误,见下面的移植过程。

> 参考：[http://blog.csdn.net/u012876599/article/details/51602101](http://blog.csdn.net/u012876599/article/details/51602101)
>   [http://blog.csdn.net/rickypc/article/details/6014408](http://blog.csdn.net/rickypc/article/details/6014408) [http://blog.csdn.net/wangxvfeng101/article/details/47002853](http://blog.csdn.net/wangxvfeng101/article/details/47002853)
>   [http://www.cnblogs.com/zhuyutian/articles/5651689.html](http://www.cnblogs.com/zhuyutian/articles/5651689.html)

五、移植过程

从QT4.8.5移植到QT5.7，中间出了问题，有一处是error "BOOST_PARAMETER_MAX_ARITY must be at least 12 for CGAL::Mesh_3"，是C:\dev\CGAL-4.8.1\include\CGAL\Mesh_3\global_parameters.h中大概33行左右和C:\dev\CGAL-4.8.1\boost\parameter\config.hpp第11行左右引起的，大概是说BOOST_PARAMETER_MAX_ARITY至少要为12，好像源码中是1或8吧。。

我在C:\dev\CGAL-4.8.1\boost\parameter\config.hpp第7行后面，添加了一个宏定义# define BOOST_PARAMETER_MAX_ARITY 12 。这会引起一个警告说宏BOOST_PARAMETER_MAX_ARITY重复定义，但只是个警告，程序能运行起来。。

有些地方使用了QInputDialog::getInteger()函数，但是在QT5中老是报错，听说是QT5中要用QInputDialog::getInt()，我就改成QInputDialog::getInt()，就好了。

还有algorith模板中的min()函数,原来项目中用min(int , unsigned int)，好像可以运行,现在在vs2015下，说min找不到重载，我就把min()的第二个参数强制转化成int，程序最终到运行起来了。