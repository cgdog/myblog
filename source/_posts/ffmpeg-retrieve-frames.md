---
title: ffmpeg 提取视频帧等基本操作
tags:
  - ffmpeg
id: 227
categories:
  - CG
date: 2016-06-02 20:32:05
---

我的操作系统为ubuntu14.04 64位 ffmpeg 2.4.3是用下面的命令安装的：


``` bash
sudo add-apt-repository ppa:kirillshkrogalev/ffmpeg-next
sudo apt-get update
sudo apt-get install ffmpeg
```


> 参考：[https://www.douban.com/note/521352400/](https://www.douban.com/note/521352400/)

1 剪切出输入视频中的一段某一段：

``` bash
ffmpeg -ss 0:0:10 -t 0:0:15  -i v18.mp4 -vcodec copy -acodec copy output.mp4
// -ss 表示开始时间（10秒处），-t持续时间,-i 输入视频(v18.mp4),-f输出格式
```


2 抽取视频帧

``` bash
ffmpeg -i v18.mp4 -r 1 -f image2 ./pic/pic_%03d.jpg
// -i 输入视频(v18.mp4)，-r 帧率，每秒抽取的帧数（1fps，从源视频里每隔一秒抽取一帧图像输出到目标文件），-f输出格式
```


3 使用ffmpeg，把视频中的一段转化成gif图片

``` bash
ffmpeg -ss 0:0:10 -t 0:0:2  -i v18.mp4 -r 1 -s 320x240 -f gif test3.gif
// -s 图像的大小(320乘240)
```

4 FFmpeg支持的格式

``` bash
ffmpeg -formats
```

5 截取视频内任意时间点(如：10秒处)的一帧图像保存为jpg图片

``` bash
ffmpeg -ss 10  -i v18.mp4 -s 600x600 -vframes 1 -f image2 test4.jpg
```

6 将多张图片合成视频

``` bash
ffmpeg -i ./pic/pic_%04d.png outputtest.mp4
```


7 获取视频信息

``` bash
ffprobe -i v18.mp4
```

> 参考:[http://www.cnblogs.com/dwdxdy/p/3240167.html](http://www.cnblogs.com/dwdxdy/p/3240167.html) [http://blog.csdn.net/happydeer/article/details/45727227](http://blog.csdn.net/happydeer/article/details/45727227) [http://einverne.github.io/page5/](http://einverne.github.io/page5/)[http://www.lai18.com/content/2022727.html](http://www.lai18.com/content/2022727.html)