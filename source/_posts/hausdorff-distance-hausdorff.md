---
title: Hausdorff distance (Hausdorff距离)
id: 486
categories:
  - math
date: 2016-09-27 11:35:11
tags:
---

本文转载自**Time Gambler**在cnblogs的文章[例说Hausdorff距离](http://www.cnblogs.com/xlz10/p/3929119.html)：[http://www.cnblogs.com/xlz10/p/3929119.html](http://www.cnblogs.com/xlz10/p/3929119.html)

给定欧氏空间中的两点集$A=\lbrace a_1, a_2, \cdots\rbrace$，$B=\lbrace b_1, b_2, \cdots\rbrace$,Hausdorff距离就是用来衡量这两个点集间的距离。 $$H(A,B)=max[h(A,B),h(B,A)]$$

　　其中，$h(A,B)= \max\limits_{a\in A}\min\limits_{b\in B}\parallel a-b\parallel $, $h(B,A)= \max\limits_{b\in B}\min\limits_{a\in A}\parallel b-a\parallel $。 $H(A,B)$称为双向Hausdorff距离， $h(A,B)$称为从点集A到点集B的单向Hausdorff距离。相应地,$h(B,A)$称为从点集B到点集A的单向Hausdorff距离。

下面从一个例子来理解Hausdorff距离。

![](http://images.cnitblog.com/blog/658135/201408/221152467686616.png)

上图中，给出了A,B,C,D四条路径，其中路径A具体为（16-17-18-19-20），路径B具体为（1-2-3-4-9-10）。要求Hausdorff距离 ，则需要先求出单向Hausdorff距离$h(A,B)$ 和 $h(B,A)$。

　对于$h(A,B)$ ，以A中的点16为例，在路径B中的所有点中，距离点16最近的是点1，距离为3。即 $\min\limits_{b\in B}\parallel a_{(16)} - b \parallel = 3$。同理由图可得 $\min\limits_{b\in B}\parallel a_{(17)} - b \parallel = 3$， $\min\limits_{b\in B}\parallel a_{(18)} - b \parallel = 3$， $\min\limits_{b\in B}\parallel a_{(19)} - b \parallel = 2$，$\min\limits_{b\in B}\parallel a_{(20)} - b \parallel = 2$ 。在它们中，值最大的为3，故 $h(A,B)=3$。

　　同理可得， $h(B,A)=4$。

　　所以 $H(A,B)=max[h(A,B),h(B,A)]=4$。

　　同理可求出上图中四条路径间的单向Hausdorff距离如下表所示：

![](http://images.cnitblog.com/blog/658135/201408/221207402378209.png)

双向Hausdorff距离$H(A,B)$ 是单向Hausdorff距离 $h(A,B)$和$h(B,A)$ 两者中的较大者，显然它度量了两个点集间的最大不匹配程度。

![](http://images.cnitblog.com/blog/658135/201408/221210044405531.png)

　当A,B都是闭集的时候，Hausdorff距离满足度量的三个定理：

　　(1) $H(A,B) \ge 0$，当且仅当A=B时， $H(A,B)=0$。

　　(2) $H(A,B)=H(B,A)$

　　(3) $H(A,B) + H(B,C) \ge H(A,C)$

　　若凸集A,B满足$A \not\subset$ B且 $B \not\subset A$，并记 $\partial A$, $\partial B$， 分别为A,B边界的点集合，则A,B的Hausdorff距离等于$\partial A$, $\partial B$ 的Hausdorff距离。
</p></p>

　　Hausdorff距离易受到突发噪声的影响。

![](http://images.cnitblog.com/blog/658135/201408/221219465965250.png)

当图像受到噪声污染或存在遮挡等情况时，原始的Haudorff距离容易造成误匹配。所以，在1933年，Huttenlocher提出了部分Hausdorff距离的概念。

　　简单地说，包含q个点的集合B与集合A的部分Hausdorff距离就是选取B中的$K$（ $K \ge 1$且$K \le q$ ）个点，然后求这K个点到A集合的最小距离并排序，则排序后的第$K$个值就是集合B到集合A的部分单向Hausdorff距离。定义公式如下： $$h_K(A,B)=K^{th}\max\limits_{a\in A}\min\limits_{b \in B}\parallel a-b\parallel$$ 　　相应地，部分双向Hausdorff距离定义为： $H_K(A,B)=max[h_K(A,B), h_K(B,A)]$