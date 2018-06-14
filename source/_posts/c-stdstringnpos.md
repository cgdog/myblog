---
title: 'C++ std::string::npos size_t易犯之错'
tags:
  - string
  - C++
id: 423
categories:
  - programming
date: 2016-09-24 10:20:41
---

**std::string::npos**的声明为**static const size_t npos = -1;**是一个静态常量。

千万不要简单地把**std::string::npos**当成**-1**，它只是在某些情况下由于类型转化而碰巧变成了**-1**。

其中类型**size_t**的解释为：**Unsigned integral type** Alias of one of the fundamental unsigned integer types.

**size_t**是无符号的，然而npos的值声明为-1。实际上npos就是机器能表示的最大整数。

在我的机器上,**size_t**其实相当于**unsigned long long**

所以，在我的机器上**std::string::npos, static const size_t npos = -1;**的值实际上等于**unsigned long long b = 0xffffffffffffffff;** 即 **18446744073709551615**。

所以，**if (std::string::npos)**这个if语句是成立的，**std::string::npos > 0**也为真。

然而，当把**std::string::npos**赋值给**int**型变量时，会变为-1。且**std::string::npos == -1**也为真。。。 看下面代码及注释：



``` cpp
#include <iostream>
using namespace std;

int main()
{
    size_t a = -1;
    cout << a << endl; // 输出：18446744073709551615
    unsigned long long b = 0xffffffffffffffff;// 最大的无符号long long的数值
    cout << b << endl;  // 输出：18446744073709551615
    string source = "abcde";
    string dest = "z";
    size_t c = source.find(dest); // c == std::string::npos
    cout << c << endl;  // 输出：18446744073709551615
        int indx = soure.find(dest);
        cout << indx << endl; // 输出：-1 
        cout << (source.find(dest) == -1) << endl;  // // 输出：1 即true
    cout << (source.find(dest) > 0) << endl; // 输出：1 即true  注意上面那条代码打印的也是1
    if (source.find(dest)) { // 会打印if， true
        cout << "if" << endl;
    }
    return 0;
}
```

### 所以，千万不要简单地把**std::string::npos**当成**-1**，它只是在某些情况下由于类型转化而碰巧变成了**-1**。如上面的代码中

```if (source.find(dest))```

和

```if (source.find(dest) == -1)```

效果是不同的。。有时是相反的。

================


``` cpp
string s = "";
```

则:s.size() == 0，

然而，


``` cpp
s.size() - 9 < 0
```

为false。在我的机器上运行，`s.size()-9`值为`18446744073709551607`。

打印`sizeof(s.size()-9)`，值为8，而不是4说明是long long，且无符号。

若是`if (s.size()-9 < 0)`，则if永远不成立。。

可以这样解决:


``` cpp
int n = s.size(); // 关键，先转化为int类型
if (n-9 < 0) { // 此时if成立了。
// do something.
}
```