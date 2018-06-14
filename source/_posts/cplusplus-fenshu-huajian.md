---
title: c++ 分数化简成最简形式
id: 360
categories:
  - algorithm
date: 2016-09-10 18:01:11
tags:
  - math
---

输入两个int型整数a, b，分别表示分子分母，即a/b。输出a/b的约分最简形式(仍然是x/y分数形式，用字符串表示). 实际上就是求出a,b的最大公约数g，(a/g)/(b/g)，即为所求。



``` cpp
#include &lt;iostream>
using namespace std;

int gcd(int a, int b) {
    return b == 0? a : gcd(b, a % b);
}

int main() {
    int a,b;
    cin >> a >> b;
    int g = gcd(a,b);
    cout &lt;&lt; a / g &lt;&lt; "/" &lt;&lt; b / g &lt;&lt; endl;
    return 0;
}
```