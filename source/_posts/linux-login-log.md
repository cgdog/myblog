---
title: linux 查看登陆日志
id: 132
categories:
date: 2016-05-21 21:50:27
tags:
  - linux
  - ubuntu
---

使用last命令，即可显示出登陆的用户，登陆时间，登陆IP。



``` bash
lei@ubuntu:~$ last
lei      pts/0        167.66.95.219     Sat May 21 21:44   still logged in   
lei      pts/0        167.66.95.219     Sat May 21 15:02 - 15:08  (00:06)    
lei      pts/0        169.66.97.99      Fri May 20 22:02 - 22:54  (00:52)    
lei      pts/0        167.121.81.100   Thu May 19 17:41 - 20:55  (03:13)    
lei      pts/0        167.121.81.100   Wed May 18 14:40 - 15:03  (00:22)    
lei      pts/0        167.66.97.99      Tue May 17 23:19 - 23:32  (00:13)    
lei      pts/0        185.173.56.141   Tue May 17 19:48 - 20:12  (00:24)    
lei      pts/0        167.121.81.100   Tue May 17 16:07 - 17:20  (01:13)    
lei      pts/0        167.121.81.100   Sun May 15 13:05 - 17:31  (04:26)    
lei      pts/1        167.66.97.99      Sat May 14 23:25 - 00:52  (01:26)    
lei      pts/0        167.121.81.100   Sat May 14 20:06 - 01:01  (04:55)    
lei      pts/0        167.121.81.100   Sat May 14 16:01 - 20:03  (04:01)    
lei      tty1                          Sat May 14 15:43 - 15:47  (00:03)    
root     tty1                          Sat May 14 15:41 - 15:43  (00:01)    
lei      pts/0        167.121.81.100   Wed May 11 21:25 - 21:25  (00:00)    
root     pts/2        167.121.81.100   Wed May 11 19:07 - 21:24  (02:16)    
root     pts/0        167.121.81.100   Wed May 11 19:03 - 21:23  (02:20)    
root     pts/1        167.121.81.100   Wed May 11 14:52 - 21:13  (06:21)    
root     tty1                          Wed May 11 10:58 - 11:03  (00:04)    
root     pts/0        167.121.81.100   Wed May 11 10:57 - 11:29  (00:32)    
reboot   system boot  3.13.0-65-generi Wed May 11 10:56 - 21:44 (10+10:48)  
reboot   system boot  3.13.0-65-generi Wed May 11 10:00 - 10:54  (00:54)    
```

> 参考:[http://www.2cto.com/os/201210/163411.html](http://www.2cto.com/os/201210/163411.html)
>   为了保护隐私，以上IP经过手动修改。。。