---
title: 解决VS2015调试时显示“正在为....dll加载符号”并需等待很长时间
id: 673
categories:
date: 2016-11-08 12:03:25
tags:
  - VS
---

最近几天，我用Visual Studio2012调试时，下面状态栏上显示“正在为....dll加载符号...”，然后需要等待很长时间才能出结果。

解决方法：
在VS上依次点【工具】【选项】【调试】【符号】，勾掉【Microsoft符号服务器】，点下面的【清空符号缓存(E)】,确定即可。

> 参考：[http://blog.sina.com.cn/s/blog_59e0b9670101doru.html](http://blog.sina.com.cn/s/blog_59e0b9670101doru.html)