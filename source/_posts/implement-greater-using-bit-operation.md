---
title: 位操作实现大于号
tags:
  - bit operation
id: 417
categories:
  - programming
date: 2016-09-23 11:24:29
---

不用大于号、小于号和if语句实现两个整形数大小的比较

1、分别取出a和b的符号
2、若a、b异号，则返回a的符号的补；否则，返回b-a的符号
定义的宏如下：



``` cpp
#define SIGN(a)    ((a>>(sizeof(int)*8-1))&0x1)
#define GRT(a,b)    (((SIGN(a)^SIGN(b))&&(!SIGN(a)))||(!(SIGN(a)^SIGN(b))&&SIGN(b-a)))
```

转自：[http://blog.chinaunix.net/uid-625789-id-2720843.html](http://blog.chinaunix.net/uid-625789-id-2720843.html)