---
title: C++中main函数执行完后还会执行完其他语句吗？
id: 689
categories:
  - programming
date: 2016-11-14 10:59:43
tags:
  - C++
---

是的 还会执行其它程序。



``` cpp
    #include &lt;iostream&gt;
    using namespace std;

    class T {
    public:
        ~T() {
            cout &lt;&lt; "~T()" &lt;&lt; endl;
        }
    };
    T t;

    void fn1()
    {
        printf("调用函数fn1()...\n");
    }
    void fn2()
    {
        printf("调用函数fn2()...\n");
    }

    int main() {

        cout &lt;&lt; "hello world" &lt;&lt; endl;
        atexit(fn1);
        atexit(fn2);
        printf("主程序正在退出...\n");
        system("pause");
        return 0;
    }
```

    程序输出(在命行下运行程序):

    <pre>`E:\vscode\ConsoleApplication2\x64\debug&gt; .\ConsoleApplication2.exe
    hello world
    主程序正在退出...
    请按任意键继续. . .
    调用函数fn2()...
    调用函数fn1()...
    ~T()
    `</pre>

    “C程序的执行是从main函数开始的，也是在main函数中结束整个程序的运行”。首先要说明一下，这句话是不正确的。严格意义上来说，程序开始运行的标识是程序的某一个制定的函数开始被调用。至于程序在哪个函数结束，C语言从来没有任何规定。

    main结束不代表整个进程结束

    （1）全局对象的构造函数会在main 函数之前执行，

    全局对象的析构函数会在main函数之后执行；

    用atexit注册的函数也会在main之后执行。

    （2）一些全局变量、对象和静态变量、对象的空间分配和赋初值就是在执行main函数之前,而main函数执行完后，还要去执行一些诸如释放空间、释放资源使用权等操作

    （3）进程启动后，要执行一些初始化代码（如设置环境变量等），然后跳转到main执行。全局对象的构造也在main之前。

    atexit()函数

    <pre>`     函数声明：int atexit(void （*func)(void));

atexit()函数来注册程序正常终止时要被调用的函数。

atexit()函数的参数是一个函数指针，函数指针指向一个没有参数也没有返回值的函数。atexit()的函数原型是：int atexit (void (*)(void));

在一个程序中最少可以调用atexit()注册32个处理函数(不同的平台编译器，数量不同)，这些处理函数的调用顺序与其注册的顺序相反，也即最先注册的最后调用，最后注册的最先调用。

> Particular library implementations may impose a limit on the number of functions call that can be registered with atexit, but this cannot be less than 32 function calls.

一个函数可以被注册多次。

> 参考：[http://blog.csdn.net/ziyuzhao123/article/details/36185519](http://blog.csdn.net/ziyuzhao123/article/details/36185519)
>   [http://www.cplusplus.com/reference/cstdlib/atexit/](http://www.cplusplus.com/reference/cstdlib/atexit/)