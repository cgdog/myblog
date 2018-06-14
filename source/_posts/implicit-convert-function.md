---
title: 隐式转换函数
id: 838
categories:
  - C++
date: 2017-03-15 23:04:14
tags:
---



``` cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class B {
   public: 
  operator string() {
    string str = "Base class.";
    return str;
  }
};

class Test {
  public:
  operator B() {
    B b;
    return b;
  }
  operator double() {
    return 520;
  }
};

int main() {
  Test t;
  double d = t - 110;
  B b = t;
  string str = b;
  cout << str << endl;
  cout << d << endl;
  return 0;
}
```

输出：

```
Base class.
410
```