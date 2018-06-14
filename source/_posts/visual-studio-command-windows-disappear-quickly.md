---
title: Visual Studio控制台程序输出窗口一闪而过的解决方法
id: 616
categories:
  - 未分类
date: 2016-10-17 17:26:01
tags:
---

我用VS2015，运行一个控制台程序，黑框一闪需过。

以前，我用vs2012时也遇到过，我只是在return 0之前了个system("pause"); 来解决了，但总觉得不舒服。

解决方法:   在工程上右键--->属性--->配置属性--->连接器--->系统--->子系统（在窗口右边）--->下拉框选择控制台(/SUBSYSTEM:CONSOLE)

> 参考：[http://blog.163.com/xh_ding/blog/static/193903289201309103539647/](http://blog.163.com/xh_ding/blog/static/193903289201309103539647/)