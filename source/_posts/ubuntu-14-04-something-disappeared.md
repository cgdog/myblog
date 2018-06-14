---
title: ubuntu 14.04 系统设置内好多东西没有了
id: 121
categories:
  - ubuntu
date: 2016-05-16 10:42:22
tags:
---

我安装的是Ubuntu14.04英文版，然后安装了五笔拼音输入法，想换一下桌面背景，结果打开系统设置，里面好多东西没有了。

原因是在安装五笔输入法时，按照网上的教程卸载了ibus，好像是unity-control-center依赖ibus。所以，以后不要卸载ibus了。

修复方法如下：

``` bash
sudo apt-get install unity-control-center
```

> 参考：[Ubuntu中文论坛](http://forum.ubuntu.org.cn/viewtopic.php?p=3076772)