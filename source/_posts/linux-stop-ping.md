---
title: Linux禁止Ping方法
tags:
  - linux
  - ping
id: 687
categories:
  - linux
date: 2016-11-12 19:44:23
---

使用iptables限制,禁止他人Ping本机的同时，本机也可以Ping他人.

设置方法, 在SSH中输入以下命令，回车后直接生效无需重启iptables



``` bash
    iptables -A INPUT -p icmp --icmp-type 8 -s 0/0 -j DROP
```

    解除设置方法（即删除本规则）:



 ``` bash
 iptables -D INPUT -p icmp --icmp-type 8 -s 0/0 -j DROP
 ```

> 参考：[http://www.kwx.gd/CentOSApp/BanPing-IPv4.html](http://www.kwx.gd/CentOSApp/BanPing-IPv4.html)