---
title: 求逆矩阵
id: 93
categories:
  - math
date: 2016-05-15 21:33:10
tags:
---

逆矩阵（英语：inverse matrix）：在线性代数中，给定一个n阶方阵$A$，若存在一n阶方阵$B$，使得$AB=I_n$，其中$I_n$是单位阵，则称$A$是可逆的且$B$是其逆矩阵。

只有方阵才有逆矩阵，若$A$是可逆矩阵，则$A$是非奇异矩阵。

**求法** - 方法一：使用伴随矩阵 若$A$可逆，则 $A^{-1} = \frac{A^{&#42;}}{|A|}$ ，其中 $A^{&#42;}$ 是 $A$ 的伴随矩阵

*   方法二：使用初等变换 举例说明： $A= \begin{bmatrix} 1 &amp; \frac{1}{2} &#92;&#92; \frac{1}{2} &amp; \frac{1}{3} &#92;&#92; \end{bmatrix} $，则求$A$的逆阵的过程如下：

\begin{bmatrix} 1 &amp; \frac{1}{2} &amp; 1 &amp; 0 &#92;&#92; \frac{1}{2} &amp; \frac{1}{3} &amp; 0 &amp; 1\ &#92;&#92; \end{bmatrix}

= \begin{bmatrix} 1 &amp; \frac{1}{2} &amp; 1 &amp; 0&#92;&#92; 0 &amp; \frac{1}{12} &amp; \frac{-1}{2} &amp; 1 &#92;&#92; \end{bmatrix}

= \begin{bmatrix} 2 &amp; \frac{1}{2} &amp; 1 &amp; 0 &#92;&#92; 0 &amp; 1 &amp; -6 &amp; 12 &#92;&#92; \end{bmatrix}

= \begin{bmatrix} 1 &amp; 0 &amp; 4 &amp; -6 &#92;&#92; 0 &amp; 1 &amp; -6 &amp; 12 &#92;&#92; \end{bmatrix}

$\therefore$ $A^{-1}$为：

\begin{bmatrix} 4 &amp; -6 &#92;&#92; -6 &amp; 12 &#92;&#92; \end{bmatrix}

> 参考：维基百科：[https://zh.wikipedia.org/wiki/%E9%80%86%E7%9F%A9%E9%98%B5](https://zh.wikipedia.org/wiki/%E9%80%86%E7%9F%A9%E9%98%B5)