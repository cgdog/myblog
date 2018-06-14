---
title: 最小二乘法
id: 195
categories:
  - math
date: 2016-05-29 14:15:28
tags:
---

最小二乘法（又称最小平方法）是一种数学优化技术。它通过最小化误差的平方和寻找数据的最佳函数匹配。

利用最小二乘法可以简便地求得未知的数据，并使得这些求得的数据与实际数据之间误差的平方和为最小。

最小二乘法还可用于曲线拟合。

其他一些优化问题也可通过最小化能量或最大化熵用最小二乘法来表达。

## 示例

![最小二乘法示例](http://www.tcp-ip.top/wp-content/uploads/2016/05/279px-Linear_least_squares_example2.svg_.png)

某次实验得到了四个数据点 (x, y)：(1, 6)、(2, 5)、(3, 7)、(4, 10)（上图中红色的点）。我们希望找出一条和这四个点最匹配的直线 y=\beta_1+\beta_2 x，即找出在某种“最佳情况”下能够大致符合如下超定线性方程组的 \beta_1 和 \beta_2：

\begin{alignat}{4} \beta_1 + 1\beta_2 &amp;&amp;\; = \;&amp;&amp; 6 &amp; \ \beta_1 + 2\beta_2 &amp;&amp;\; = \;&amp;&amp; 5 &amp; \ \beta_1 + 3\beta_2 &amp;&amp;\; = \;&amp;&amp; 7 &amp; \ \beta_1 + 4\beta_2 &amp;&amp;\; = \;&amp;&amp; 10 &amp; \ \end{alignat} 最小二乘法采用的手段是尽量使得等号两边的方差最小，也就是找出这个函数的最小值：

\begin{align} S(\beta_1, \beta_2) = &amp;\left[6-(\beta_1+1\beta_2)\right]^2+\left[5-(\beta_1+2\beta_2) \right]^2 \ &amp;+\left[7-(\beta_1 + 3\beta_2)\right]^2+\left[10-(\beta_1 + 4\beta_2)\right]^2.\ \end{align} 最小值可以通过对 S(\beta_1, \beta_2) 分别求 \beta_1 和 \beta_2 的偏导数，然后使它们等于零得到。

$\frac{\partial S}{\partial \beta_1}=0=8\beta_1 + 20\beta_2 -56 \frac{\partial S}{\partial \beta_2}=0=20\beta_1 + 60\beta_2 -154$. 如此就得到了一个只有两个未知数的方程组，很容易就可以解出：

$\beta_1=3.5 \beta_2=1.4 $也就是说直线 $y=3.5+1.4x$ 是最佳的。

> 参考：[维基百科](https://zh.wikipedia.org/wiki/%E6%9C%80%E5%B0%8F%E4%BA%8C%E4%B9%98%E6%B3%95)