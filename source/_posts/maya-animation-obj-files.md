---
title: maya 使用几个.obj文件，创建动画，每个.obj文件对应一帧
id: 357
categories:
  - CG
date: 2016-09-01 22:16:15
tags:
  - Maya
---

我有几个.obj文件，想用它们做成动画视频（.avi格式)，每一个.obj是一个mesh，对应一帧，且每一帧只显示一个mesh。

maya 使用几个.obj文件，创建动画，每个.obj文件对应一帧

我在Yutube上看到一个导入/导出 OBJ Sequences的教程：[Autodesk Maya Tool - OBJ Sequence Import/Export demo](https://www.youtube.com/watch?v=Fl2NplM1ih4)。 这个教程中提供了一个maya的mel脚本文件：[OBJ Sequences Import/Export 2.0.3 (maya script)](https://www.creativecrash.com/maya/script/obj-animation-exporter)。

1、首先打开maya，默认有了一个场景，导入下载的脚本：文件->导入... ，选择刚才下载的craOBJSequences.mel文件 2、在maya底部的MEL命令框里，输入craOBJSequences，就可以按视频教程上的方式导入准备好的.obj文件了。

然后，发现点击下方时间轴右边的“向后播放按钮”，已经形成动画了。然后，我在“渲染模式”下，设置了视频的导出的格式为.avi，起始、终止帧等，批量渲染，就生成了视频。

maya导出.avi视频的方法：[http://wenwen.sogou.com/z/q169988993.htm](http://wenwen.sogou.com/z/q169988993.htm)

我在gamedev.stackexchange.com也提问了，自问自答了。[How to create an animation from several .obj files in maya?](http://gamedev.stackexchange.com/questions/129295/how-to-create-an-animation-from-several-obj-files-in-maya/129298#129298)

感谢热心网友、大神。