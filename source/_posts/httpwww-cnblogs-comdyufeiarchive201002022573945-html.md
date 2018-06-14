---
title: 'http://www.cnblogs.com/dyufei/archive/2010/02/02/2573945.html'
id: 768
categories:
date: 2016-12-26 22:59:53
tags:
  - windows
---

# 无法解析的外部符号 _WinMain@16

本文转自： http://www.cnblogs.com/dyufei/archive/2010/02/02/2573945.html

## 无法解析的外部符号 _WinMain@16

Ctrl+F7 编译的时候没有错误，而F6生成解决方案的时候出现如下两个错误：

1：error LNK2019: 无法解析的外部符号 _WinMain@16，该符号在函数 ___tmainCRTStartup 中被引用        MSVCRTD.lib

2： error LNK1120: 1 个无法解析的外部命令

出这个错误可能有以下几个原因：
一、新建项目是控制台应用程序而程序通过的是WinMian（及windows入口函数）

因为新建项目的时候选择的是控制台应用程序，控制台应用程序的入口是main。而在.CPP文件中提供的是windows入口函数WinMian。

解决办法：

（1）项目->属性->配置属性->C/C++ ->预处理器 中的【预处理器定义】 删除“_CONSOLE” 添加 “ _WINDOWS”

（2）项目->属性->配置属性->连接器->系统中的【子系统】设置为Windows(/SUBSYSTEM:WINDOWS)

（3）生成->重新生成解决方案

二、WinMain的UNICODE版和ANSI版不匹配

为了支持UNICODE,C运行库对WinMain其实区分了UNICODE版和ANSI版。对UNICODE版的程序,C运行库调用wWinMain,而对于ANSI版的则调用WinMain。

解决办法：

（1）将代码中的 int APIENTRY _tWinMain 替换为 INT WINAPI wWinMain （INT WINAPI wWinMain 替换为 int APIENTRY _tWinMain ）

（2）生成->重新生成解决方案