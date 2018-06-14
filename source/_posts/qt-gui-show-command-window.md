---
title: QT-GUI程序显示命令行调试窗口
id: 629
categories:
  - QT
date: 2016-10-22 21:59:59
tags:
---

[QT-GUI程序显示命令行调试窗口](http://www.cnblogs.com/kekec/archive/2012/02/12/2347784.html)

我用vs2015写QT GUI程序，不显示命令框，无法用std::cout打印信息。项目中没有了.pro文件。 解决方案：

修改工程属性配置 Linker - System - SubSystem

Windows (/SUBSYSTEM:WINDOWS) ->Console (/SUBSYSTEM:CONSOLE)

参考：[http://www.cnblogs.com/kekec/archive/2012/02/12/2347784.html](http://www.cnblogs.com/kekec/archive/2012/02/12/2347784.html)