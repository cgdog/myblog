---
title: 第2章 感知机
categories:
  - machine learning
date: 2017-5-27 9:39:22
tags:
---

**感知机(perceptron)**是二类分类的线性分类模型，其输入为实例的特征向量，输出为实例的类别，取$+1$和$-1$二值。感知机对应于输入空间(特征空间)中将实例划分为正负两类的分离超平面，属于判别模型。感知机学习旨在求出将训练数据进行线性划分的分离超平面，为此，导入基于误分类的损失函数，利用梯度下降法对损失函数进行极小化，求得感知模型。

感知机学习算法具有简单而易于实现的优点，分为原始形式和对偶形式。感知机模型1957年由Rosenblatt提出，是神经网络与支持向量机的基础。

## 2\.1 感知机模型

**定义 2.1 (感知机)** 假设输入空间(特征空间)是$\mathcal{X}\subseteq R^n$，输出空间是$\mathcal{y}=\lbrace +1,-1\rbrace$。输入$x\in\mathcal{X}$表示实例的特征向量，对应于输入空间(特征空间)中的点；输出$y\in\mathcal{Y}表示实例的类别$。由输入空间到输出空间的如下函数 $$f(x)=sign(w\cdot x+b)$$ 称为感知机。其中，$w$和$b$为感知机模型参数，$w\in R^n$叫作权值(weight)或权向量(weight vector)，$b\in R$叫作偏置(bias)，$w\cdot x$表示$w$和$x$的内积。sign是符号函数，即 \begin{eqnarray} sign(x)= \begin{cases}+1, \mbox{$x\geq 0$} \newline -1, \mbox{$x < 0$} \end{cases} \end{eqnarray}

感知机是一种线性分类模型，属于判别模型。感知机模型的假设空间是定义在特征空间中的所有线性分类模型(linear classification model)或线性分类器(linear classifier)，即函数集合$\lbrace f|f(x)=w\cdot x + b \rbrace$。

感知机有如下几何解释：线性方程 $$w\cdot x + b = 0$$ 对应于特征空间$R^n$中的一个超平面$S$，其中$w$是超平面的法向量，$b$是超平面的截距。此超平面将特征空间划分为两个部分。位于两部分的点(特征向量)分别被分为正、负两类。因此，超平面$S$被称为分享超平面(separating hyperplane)。

![感知机模型][1]

## 2\.2 感知机学习策略

损失函数的一个自然选择是误分类点的总数。但是，这样的损失函数不是参数$w$,$b$的连续可导函数，不易优化。损失函数的另一个选择是误分类点到超平面$S$的总距离，这是感知机所采用的。

输入空间$R^n$中任一点$x_0$到超平面$S$的距离： $$\frac{1}{\parallel w\parallel}|w\cdot x_0 + b|$$ 这里，$\parallel w\parallel$是$w$的范数。

对于误分类的数据$(x_i, y_i)$来说， $$-y_i (w\cdot x_i + b) > 0$$ 成立。因为当$w\cdot x_i + b > 0$时，$y_i = -1$，而当$w\cdot x_i + b < 0$时，$y_i = +1$。因此，**误分类点**$x_i$到超平面$S$的距离是 $$-\frac{1}{\parallel w\parallel}y_i (w\cdot x_i +b)$$

这样，假设平面$S$的误分类点集合为$M$，那么所有误分类点到超平面$S$的总距离为 $$-\frac{1}{\parallel w\parallel}\sum_{x_i \in M}y_i (w\cdot x_i + b)$$ 不考虑\frac{1}{\parallel w\parallel}，就得到感知机学习的损失函数，即： $$L(w,b)=-\sum_{x_i\in M}y_i (w\cdot x_i + b)$$ 其中$M$为误分类点的集合。这个损失函数就是感知机学习的经验风险函数。

损失函数是非负的。若没有误分类点，损失函数值为$0$。而且，误分类点越少，误分类点离超平面越近，损失函数值就越小。一个特定的样本点的损失函数：在误分类时是参数$w$,$b$的线性函数，在正确分类时是$0$。因此，给定训练数据集$T$，损失函数$L(w,b)$是$w$，$b$的连续可导函数。

## 2\.3 感知机学习算法

### 2\.3.1 感知机学习算法的原始形式

感知机学习算法是对以下最优化问题的算法。给定一个训练数据集 $$T=\lbrace (x_1,y_1), (x_2, y_2), \cdots, (x_N, y_N) \rbrace$$ 其中，$x_i\in \mathcal{X}=R^n$，$y_i\in\mathcal{Y}=\lbrace -1, 1 \rbrace, i=1,2,\cdots,N$，求参数$w$,$b$，使其为以下损失函数极小化问题的解 $$\underset{w,b}{\min}L(w,b)=-\sum_{x_i\in M}y_i(w\cdot x_i + b)$$ 其中$M$为误分类点的集合。

感知机学习算法是误分类驱动的，具体采用**随机梯度下降法(stochastic gradient descent)** 。首先，任意选取一个超平面$w_0$，$b_0$，然后用梯度下降法不断地极小化目标函数。极小化过程中不是一次使$M$中所有误分类点的梯度下降，而是一次随机选取一个误分类点使其梯度下降。

假设误分类点集合$M$是固定的，那么损失函数$L(w,b)$的梯度由 $$\nabla_{w}L(w,b)=-\sum_{x_i\in M}y_i x_i$$ $$\nabla_{b} L(w,b)=-\sum_{x_i\in M}y_i$$ 给出。

随机选取一个误分类点$(x_i,y_i)$，对$w$,$b$进行更新： $$w\leftarrow w+\eta y_i x_i$$ $$b\leftarrow b+\eta y_i$$ 式中$\eta$是步长。在统计学习中又称为**学习率(learning rate)**。这样，通过迭代可以期待损失函数$L(w,b)$不断减小，直到为$0$。

综上所述，得到如下算法：

**算法2.1 (感知机学习算法的原始形式)**  
输入：训练数据集$T=\lbrace (x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N) \rbrace$，其中$x_i\in\mathcal{X}=R^n$,$y_i\in\mathcal{Y}=\lbrace -1,+1 \rbrace,i=1,2,\cdots,N$；学习率$\eta (0<\eta\leq 1)$;  
输出：$w,b$；感知机模型$f(x)=sign(w\cdot x +b)$.  
(1) 选取初值$w_0,b_0$  
(2) 在训练集中选取数据$(x_i,y_i)$  
(3) 如果$y_i(w\cdot x_i +b)\leq 0$  
$$w\leftarrow w+\eta y_i x_i$$ $$b\leftarrow b + \eta y_i$$ (4) 转至(2)，直至训练集中没有误分类点。

这种学习算法的直观解释：当一个实例点被误分类，即位于分离超平面的错误一侧时，则调整$w,b$的值，使分离超平面向该误分类点的一侧移动，以减少该误分类点与超平面间的距离，直到超平面越过该误分类点使其被正确分类。

### 2\.3.2 算法的收敛性

当训练数据集是线性可分时，感知机学习算法原始形式迭代是收敛的。当训练集线性不可分时，感知机学习算法不收敛，迭代结果会发生震荡。

### 2\.3.3 感知机学习算法的对偶形式

对偶形式的基本想法是，将$w$和$b$表示为实例$x_i$和标记$y_i$的线性组合的形式，通过求解其系数而求得$w$和$b$。

感知机学习算法的对偶形式迭代是收敛的，存在多个解。

 [1]: http://oqfqjieze.bkt.clouddn.com/perceptron.png