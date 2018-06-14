---
title: python 默认参数陷井
id: 620
categories:
  - python
date: 2016-10-18 22:27:20
tags:
---

这简直就是Bug。。



``` python
def extend_list(val, list=[]):
    list.append(val)
    return list

list1 = extend_list(10)
list2 = extend_list(123, [])
list3 = extend_list('a')

print(list1) # list1 = [10, 'a']
print(list2) # list2 = [123]
print(list3) # list3 = [10, 'a']
```

> Reference: [http://cenalulu.github.io/python/default-mutable-arguments/](http://cenalulu.github.io/python/default-mutable-arguments/)
> 
>   [http://www.cnblogs.com/Lands-ljk/p/5836492.html](http://www.cnblogs.com/Lands-ljk/p/5836492.html)