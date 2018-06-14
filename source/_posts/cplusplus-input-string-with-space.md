---
title: C++ 输入一个带有空格的字符串
tags:
  - c++
  - string
id: 397
categories:
  - 未分类
date: 2016-09-18 17:34:56
---

```
#include <iostream>
#include &lt;fstream>
using namespace std;

int main()
{ 
  char str[20];
  cin.getline(str, 19);
  cout << str << endl;
  return 0;
}
```

若字符串是string类型的，有如下写法：

**getline读取一行**

C++中定义了一个在std名字空间的全局函数getline，因为这个getline函数的参数使用了string字符串，所以声明在了&lt; string>头文件中了。

getline利用cin可以从标准输入设备键盘读取一行，当遇到如下三种情况会结束读操作：1）到文件结束，2）遇到函数的定界符，3）输入达到最大限度。

函数原型有两个重载形式：



``` cpp
istream& getline ( istream& is, string& str);//默认以换行符结束
istream& getline ( istream& is, string& str, char delim);
``


``` cpp
#include <iostream>
#include <string>
using namespace std;

int main()
{
  string str;
  getline(cin, str);
  cout &lt;&lt; str &lt;&lt; endl;

  return 0;
}
```

> 参考：[http://www.voidcn.com/blog/qq_23968185/article/p-5739468.html](http://www.voidcn.com/blog/qq_23968185/article/p-5739468.html)
> 
> [http://blog.csdn.net/k346k346/article/details/48213811](http://blog.csdn.net/k346k346/article/details/48213811)