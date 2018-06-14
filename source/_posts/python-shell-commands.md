---
title: python中执行shell命令
id: 269
categories:
  - python
date: 2016-06-14 15:42:31
tags:
---

1 os模块中的os.system()这个函数来执行shell命令(这个方法得不到shell命令的输出。)


``` python
os.system('ls')
```

2 commands模块#可以很方便的取得命令的输出（包括标准和错误输出）和执行状态位


``` python
status,output = commands.getstatusoutput('ls')
```

> 参考：[python学习——python中执行shell命令](http://zhou123.blog.51cto.com/4355617/1312791)