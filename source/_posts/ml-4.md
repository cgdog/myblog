---
title: 第4章 朴素贝叶斯法
categories:
  - machine learning
date: 2017-6-9 10:58:22
tags:
---


**朴素贝叶斯法(naive Bayes)**法是基于贝叶斯定理与特征条件独立假设的分类方法。

对于给定的训练数据集，首先基于特征条件独立假设学习输入/输出的联合概率分布；然后基于此模型，对给定的输入$x$利用贝叶斯定理求出后验概率最大的输出$y$。

## 4\.1 朴素贝叶斯法的学习与分类

### 4\.1.1 基本方法

设输入空间$\mathcal{X}\subseteq R^n$为$n$维向量的集合，输出空间为类标记集合$\mathcal{Y}=\lbrace c_1, c_2,\cdots, c_k \rbrace$.输入为特征向量$x\in \mathcal{X}$，输出为类标记(class label)$y\in\mathcal{Y}$。$X$是定义在输入空间$\mathcal{X}$上的随机变量，$y$是定义在输出空间$\mathcal{Y}$上的随机变量。$P(X,Y)$是$X$和$Y$的联合概率分布。训练数据集 $$T=\lbrace(x_1, y_1),(x_2, y_2),\cdots,(x_N, y_N) \rbrace$$ 由$P(X,Y)$独立同分布产生。

朴素贝叶斯法通过训练数据集学习联合概率分布$P(X,Y)$。具体地，学习以下先验概率分布及条件概率分布。先验概率分布： $$P(Y=c_k), k=1,2,\cdots, K$$ 条件概率分布 $$P(X=x|Y=c_k)=P(X^{(1)} = x^{(1)},\cdots,X^{(n)}=x^{(n)}|Y=c_k),k=1,2,\cdots,K$$ 于是学习到联合概率分布$P(X,Y)$。

条件概率分布$P(X=x|Y=c_k)$有指数级数量的参数，其估计实际是不可行的。事实上，假设$X^{(j)}$可取值有$S_j$个，$j=1,\cdots,n, Y$可取值有$K$个，那么参数个数为$K\prod_{j=1}^n S_j.$

朴素贝叶斯法对条件概率分布作了条件独立性的假设。由于这是一个较强的假设，朴素贝叶斯法也由此得名。具体地，条件独立性假设是 $$P(X=x|Y=c_k)=P(X^{(1)}=x^{(1)},\dots,X^{(n)}=x^{(n)}|Y=c_k) =\prod_{j=1}^{n} P(X^{(j)}=x^{(j)}|Y=c_k) $$ 朴素贝叶斯法实际上学习到生成数据的机制，所以属于生成模型。条件独立假设等于是说用于分类的特征在类确定的条件下都是条件独立的。这一假设使朴素贝叶斯法变得简单，但有时会牺牲一定的分类准确率。

朴素贝叶斯法分类时，对给定的输入$x$，通过学习到的模型计算后验概率分布$P(Y=c_k|X=x)$，将后验概率最大的类作为$x$的类输出。后验概率计算根据贝叶斯定理进行： $$P(Y=c_k|X=x)=\frac{P(X=x|Y=c_k)P(Y=c_k)}{\sum_k P(X=x|Y=c_k)P(Y=c_k)}$$

所以，

$$P(Y=c_k|X=x)=\frac{P(Y=c_k)\prod_j P(X^{(j)} = x^{(j)}|Y=c_k)}{\sum_k P(Y=c_k)\prod_j P(X^{(j)}=x^{(j)}|Y=c_k)}, k=1,2,\cdots,K$$ 这是朴素贝叶斯分类的基本公式。于是，朴素贝叶斯分类器可表示为: $$y=f(x)=\underset{c_k}{\arg\max}\frac{P(Y=c_k)\prod_j P(X^{(j)} = x^{(j)}|Y=c_k)}{\sum_k P(Y=c_k)\prod_j P(X^{(j)}=x^{(j)}|Y=c_k)}$$

注意到，上式中分母对所有$c_k$都是相同的，所以， $$y=\underset{c_k}{\arg\max}P(Y=c_k)\prod_j P(X^{(j)} = x^{(j)}|Y=c_k)$$

### 4\.1.2 后验概率最大化的含义

朴素贝叶斯法将实例分到后验概率最大的类中。这等价于期望风险最小化。假设先把0-1损失函数： $$ \begin{eqnarray} L(Y, f(X)) = \begin{cases} 1,&Y\neq f(X) \newline 0,&Y=f(X) \end{cases} \end{eqnarray} $$ 式中$f(x)$是分类决策函数。这时，期望风险函数为 $$R_{exp}(f)=E[L(Y,f(X))]$$ 期望是对联合分布$P(X,Y)$取的。由此条件期望 $$R_{exp}(f)=E_X\sum_{k=1}^{K}[L(c_k, f(X))]P(c_k|X)$$ 为了使期望风险最小化，只需对$X=x$逐个极小化，由此得到： \begin{align} f(x)&=\underset{y\in\mathcal{Y}}{\arg\min}\sum_{k=1}^{K}L(c_k,y)P(c_k|X=x)\newline &=\underset{y\in\mathcal{Y}}{\arg\min}\sum_{k=1}^{K}P(y\neq c_k|X=x)\newline &=\underset{y\in\mathcal{Y}}{\arg\min}(1-P(y=c_k|X=x))\newline &=\underset{y\in\mathcal{Y}}{\arg\max}P(y=c_k|X=x) \end{align}

这样一来，根据期望风险最小化准则就得到了后验概率最大化准则： $$f(x)=\underset{c_k} P(c_k|X=x)$$ 即朴素贝叶斯法所采用的原理。

## 4\.2 朴素贝叶斯法的参数估计

### 4\.2.1 极大似然估计

在朴素贝叶斯法中，学习意味着估计$P(Y=c_k)$和$P(X^{(j)}=x^{(j)}|Y=c_k)$。可以应用[极大似然估计法][1]估计相应的概率。先验概率$P(Y=c_k)$的极大似然估计是 $$P(Y=c_k)=\frac{\sum_{i=1}^{N}I(y_i=c_k)}{N},k=1,2,\cdots,K$$ 设第$j$个特征$x^{(j)}$可能取值的集合为$\lbrace a_{j1}, a_{j2}, \cdots, a_{jS_j} \rbrace$，条件概率$P(X^{(j)}=a_{jl}|Y=c_k)$的极大似然估计是 $$ P(X^{(j)}=a_{jl}|Y=c_k)=\frac{\sum_{i=1}^{N}I(x_i^{(j)}=a_{jl}, y_i=c_k)}{\sum_{i=1}^{N} I(y_i=c_k)}$$. $j=1,2,\cdots,n$; $l=1,2,\cdots,S_j$;$k=1,2,\cdots,K$. 式中$x_i^{(j)}$是第$i$个样本的第$j$个特征；$a_{jl}$是第$j$个特征可能取的第$l$个值；$I$为指示函数。

### 4\.2.2 学习与分类算法

**算法4.1 朴素贝叶斯算法(naive Bayes algorithm)**  
**输入：**训练数据$T=\lbrace (x_1,y_1),(x_2,y_2),\cdots,(x_N,y_N) \rbrace$，其中$x_i=(x_i^{(1)},x_i^{(2)},\cdots,x_i^{(n)})^T$，$x_i^{(j)}$是第$i$个样本的第$j$个特征，$x_i^{(j)}\in\lbrace a_{j1},a_{j2},\cdots,a_{jS_j} \rbrace$，$a_{jl}$是第$j$个特征可能取的第$l$个值，$j=1,2,\cdots,n, l=1,2,\cdots,S_j, y_i\in \lbrace c_1,c_2,\cdots,c_k \rbrace$;实例$x$;  
**输出:**实例$x$的分类。

(1)计算先验概率及条件概率  
$$ P(Y=c_k)=\frac{\sum_{i=1}^{N}I(y_i=c_k)}{N}, k=1,2,\cdots,K$$ $$ P(X^{(j)}=a_{jl}|Y=c_k)=\frac{\sum_{i=1}^N I(x_i^{(j)}=a_{jl},y_i=c_k)}{\sum_{i=1}^{N}I(y_i=c_k)}$$ $$j=1,2,\cdots,n l=1,2,\cdots,S_j k=1,2,\cdots,K$$

(2)对于给定的实例$x=(x^{(1)},x^{(2)},\cdots,x^{(n)})^T$，计算 $$P(Y=c_k)\prod_{j=1}^{n}P(X^{(j)}=x^{(j)}|Y=c_k),k=1,2,\cdots,K$$

(3)确定实例$x$的类 $$y=\underset{c_k}{\arg\max}P(Y=c_k)\prod_{j=1}^{n}P(X^{(j)}=x^{(j)}|Y=c_k)$$

### 4\.2.3 贝叶斯估计

用极大似然估计可能会出现所要估计的概率值为$0$的情况。这时会影响到后验概率的计算结果，使分类产生偏差。解决这一问题的方法是采用贝叶斯估计。

条件概率的贝叶斯估计是 $$P_{\lambda}(X^{(j)}=a_{jl}|Y=c_k)=\frac{\sum_{i=1}^NI(X^{(j)}=a_{jl},y_i=c_k)+\lambda}{\sum_{i=1}^N I(y_i=c_k)+S_j\lambda}$$ 式中$lambda\ge 0$。等价于在随机变量各个取值的频数上赋予一个正数$\lambda > 0$ 。当$\lambda = 0$时就是极大似然估计。常取$\lambda=1$，这时称为**拉普拉斯平滑(Laplace smoothing)**。显然，对任何$l=1,2,\cdots,S_j, k=1,2,\cdots,K$，有 $$P_{\lambda}(X^{(j)}=a_{jl}|Y=c_k) > 0$$ $$\sum_{l=1}^{S_j}P(X^{(j)}=a_{jl}|Y=c_k)=1$$

**Note**:$S_j$是$X^{(j)}$可能的取值个数，$K$是$Y$可能的取值个数。

## 总结

1\.朴素贝叶斯法是典型的生成学习方法。生成方法由训练数据，学习联合概率分布$P(X,Y)$，然后求得后验概率分布$P(Y|X)$。具体来说，利用训练数据学习$P(X|Y)$和$P(Y)$的估计，得到联合概率分布： $$P(X,Y)=P(Y)P(X|Y)$$ 概率估计方法可以极大似然估计或贝叶斯估计

2\.朴素贝叶斯法的基本假设是**条件独立性**，

\begin{eqnarray} P(X=x|Y=c_k) &=P(X^{(1)}=x^{(1)},\cdots,X^{(n)}=x^{(n)}|Y=c_k) \newline &=\prod_{j=1}^{n}P(X^{(j)}=x^{(1)}|Y=c_k) \end{eqnarray}

这是一个较强的假设。由于这一假设，模型包含的条件概率的数量大为减少，朴素贝叶斯法的学习与预测大为简化。因而朴素贝叶斯法高效，且易于实现。其缺点是分类的性能不一定很高。

3\.朴素贝叶斯法利用贝叶斯定理与学到的联合概率模型进行分类预测。 $$ P(Y|X)=\frac{P(X,Y)}{P(X)}=\frac{P(Y)P(X|Y)}{\sum_Y P(Y)P(X|Y)} $$ 将输入$x$分到后验概率最大的类$y$。

$$y=\underset{c_k}{\arg\max}P(Y=c_k)\prod_{j=1}^{n}P(X_j=x^{(j)}|Y=c_k)$$

后验概率最大等价于0-1损失函数时的期望风险最小化。

 [1]: https://zh.wikipedia.org/wiki/%E6%9C%80%E5%A4%A7%E4%BC%BC%E7%84%B6%E4%BC%B0%E8%AE%A1