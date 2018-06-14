---
title: Shapiro–Wilk test(夏皮罗-威尔克检验法)  p-value
id: 201
categories:
  - math
date: 2016-05-29 15:47:41
tags:
---

**Shapiro–Wilk test(夏皮罗-威尔克检验法)**是一个在频率统计(frequentist statistics)中的正态性检验,　由 Samuel Sanford Shapiro 和 Martin Wilk发明。

## 原理

Shapiro–Wilk检验使用零假设原则(null hypothesis principle)，检验一个样本$x_1, ..., x_n$是否来自一个正态分布总体。检验统计量是:

$W = {\left(\sum_{i=1}^n a_i x_{(i)}\right)^2 \over \sum_{i=1}^n (x_i-\overline{x})^2}$,

此处：

*   $x_{(i)}$表示第i个顺序统计量，即样本中第i小的数字。
*   $\overline{x} = \left( x_1 + \cdots + x_n \right) / n$ 是样本平均值。
*   常量$a_i$由$(a_1,\dots,a_n) = {m^{\mathsf{T}} V^{-1} \over (m^{\mathsf{T}} V^{-1}V^{-1}m)^{1/2}}$给定，$m = (m_1,\dots,m_n)^{\mathsf{T}}\,$和$ m_1,\ldots,m_n$是从标准正态分布中抽样的独立同分布的顺序统计量的期望值，$V$是那些顺序统计量的协方差矩阵。

如果$W$小于预先定义的阈值，用户可能拒绝零假设(null hypothesis)。

## 说明

这个测验(即Shapiro–Wilk test)的零假设是样本总体成正态分布。因此，如果p-value（即p值）小于选定的$\alpha$水平(alpha level)，则拒绝零假设，且有证据说明测试数据不来自标准正态分布总体。换句话说，数据不是正态的。相反，若p-value大于选定的$\alpha$水平，则不能拒绝零假设(即数据来自正态分布总体)。如：$\alpha$水平为0.05，数据集的p值为0.02，则拒绝零假设。 However, since the test is biased by sample size,[3] the test may be statistically significant from a normal distribution in any large samples.

## p-value(p值)

p-value是观测到的一个统计模型的样本结果(一个检验统计量)的一个函数。使用p-value的统计假设检验在许多科学和社会科学领域被使用，如：经济学、心理学、生物学、刑侦等。

### 概述

p值是观测结果与正在做的检验(test)无关的概率。特别地，p值被定义为在假定模型(零假设)是有效的情况下，获取一个结果等于正在观测的事物，或者比正在观测的事物更加“极端(more extreme)”的概率。所谓的“极端(more extreme)”有不同的定义，如下(待翻译)：

In frequentist inference, the p-value is widely used in statistical hypothesis testing, specifically in null hypothesis significance testing. In this method, as part of experimental design, before performing the experiment, one first chooses a model (the null hypothesis) and a threshold value for p, called the significance level of the test, traditionally 5% or 1% [6] and denoted as α. If the p-value is less than or equal to the chosen significance level (α), the test suggests that the observed data is inconsistent with the null hypothesis, so the null hypothesis must be rejected. However, that does not prove that the tested hypothesis is true. When the p-value is calculated correctly, this test guarantees that the Type I error rate is at most α. For typical analysis, using the standard α = 0.05 cutoff, the null hypothesis is rejected when p < .05 and not rejected when p > .05\. The p-value does not in itself support reasoning about the probabilities of hypotheses but is only a tool for deciding whether to reject the null hypothesis.

> 参考：[Shapiro–Wilk test](https://en.wikipedia.org/wiki/Shapiro%E2%80%93Wilk_test)　　[p-value](https://en.wikipedia.org/wiki/P-value)