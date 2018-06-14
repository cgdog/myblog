---
title: 检测显卡类型和OpenGL版本及opengl开发环境配置
tags:
  - opengl
  - ubuntu
id: 291
categories:
  - CG
date: 2016-07-07 20:05:23
---

1、检测DirectX：打开cmd，输入dxdiag 回车

2、检测本机支持的opengl版本：下载[OpenGL Extension Viewer](http://www.realtech-vr.com/glview/download.php),支持Windows，Mac，移动设备

> 参考：[http://blog.csdn.net/kikitamoon/article/details/8632301](http://blog.csdn.net/kikitamoon/article/details/8632301)

3、ubuntu上检测支持的opengl版本：



``` bash
glxinfo | grep OpenGL
```

可能要安装一下glxinfo：


``` bash
sudo apt-get install mesa-utils
```

我的机器输出：

``` bash
OpenGL vendor string: NVIDIA Corporation
OpenGL renderer string: GeForce GTX 650/PCIe/SSE2
OpenGL core profile version string: 4.3.0 NVIDIA 352.63
OpenGL core profile shading language version string: 4.30 NVIDIA via Cg compiler
OpenGL core profile context flags: (none)
OpenGL core profile profile mask: core profile
OpenGL core profile extensions:
OpenGL version string: 4.5.0 NVIDIA 352.63
OpenGL shading language version string: 4.50 NVIDIA
OpenGL context flags: (none)
OpenGL profile mask: (none)
OpenGL extensions:
```

4、opengl开发环境配置，参考：[在Windows/Ubuntu下安装OpenGL环境（GLUT/freeglut)与跨平台编译（mingw/g++）](http://www.cnblogs.com/joyeecheung/p/4310487.html)、[ ubuntu 14.04 安装OpenGL（基于freeglut）](http://blog.csdn.net/yxfkq/article/details/40819921)、[opengl入门（ubuntu版）（一）](http://blog.csdn.net/plc_jianghao/article/details/51154929)、[在Ubuntu下如何开发配置OpenGL环境](http://os.51cto.com/art/201109/288868.htm)