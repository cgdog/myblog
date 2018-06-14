---
title: 对称正定矩阵 (Positive-definite matrix)
id: 507
categories:
  - math
date: 2016-09-27 16:44:43
tags:
---

# 对称正定矩阵 (Positive-definite matrix)

首先是：

## 正定矩阵

正定矩阵 (英文：positive definite matrix) 有时会简称为正定阵。在双线性代数中，正定矩阵的性质类似复数中的正实数。与正定矩阵相对应的线性算子是对称正定双线性形式（复域中则对应埃尔米特正定双线性形式）。

**广义定义:**

设M是n阶方阵，如果对任何非零向量z，都有zTMz> 0，其中zT 表示z的转置，就称M正定矩阵。[1] 例如：B为n阶矩阵，E为单位矩阵，a为正实数。aE+B在a充分大时，aE+B为正定矩阵。（B必须为对称阵）

**狭义定义:**

一个n阶的实对称矩阵M是正定的当且仅当对于所有的非零实系数向量z，都有zTMz> 0。其中zT表示z的转置。

**特征及性质:**

正定矩阵在合同变换下可化为标准型， 即对角矩阵。

所有特征值大于零的对称矩阵（或厄米矩阵）也是正定矩阵。

**判定定理1：**对称阵A为正定的充分必要条件是：A的特征值全为正。

**判定定理2：**对称阵A为正定的充分必要条件是：A的各阶顺序主子式都为正。

**判定定理3：**任意阵A为正定的充分必要条件是：A合同于单位阵。

**正定矩阵的性质：**

1&#46;正定矩阵一定是非奇异的。奇异矩阵的定义：若n阶矩阵A为奇异阵，则其的行列式为零，即 |A|=0。

2&#46;正定矩阵的任一主子矩阵也是正定矩阵。

3&#46;若A为n阶对称正定矩阵，则存在唯一的主对角线元素都是正数的下三角阵L，使得A=L*L′，此分解式称为 正定矩阵的乔列斯基（Cholesky）分解。

4&#46;若A为n阶正定矩阵，则A为n阶可逆矩阵。

* * *

## 对称正定矩阵

对称正定矩阵，顾名思义，就是对称的正定矩阵，它与正定矩阵的区别就是具有对称性，是正定矩阵中的一种特殊情况，在计算方法迭代法，直接法中常被用到。

### 性质

若n阶矩阵A为对称正定矩阵，则有：$det(A)>0，A^T=A$，且A的顺序主子式$det(A_k)>0，k=1,2,...,n$

### 应用

对称正定矩阵A可进行LU分解（或称Doolittle分解）和Cholesky分解。

**LU分解**

若A为一n阶对称正定矩阵，则有：

$A=LU$

其中$L$为一单位下三角形矩阵（即主对角线元素皆为1），$U$为上三角形矩阵。且对于$A,L,U$的任意k阶主子式 $A_k，L_k ，U_k $有：

$ A_k = L_k U_k, k=1,2,...,n$

**Cholesky分解**

若A为一n阶对称正定矩阵，则存在一非奇异下三角形实矩阵L，使得： $A= LL^T$

其中L的主对角线元素皆为正，且该分解式是惟一的。

* * *

## 半正定矩阵

对一般的矩阵来说，要把矩阵化成标准型才可以这样说。一个矩阵是半正定的是指该矩阵对应的实二次型$f(x_1,x_2,\cdots,x_n)$对任意的一组不全为零的实数$c_1,c_2,\cdots,c_n$都有$f(c_1,c_2,\cdots,c_n)\ge 0$.

### 判定一个矩阵半正定

1、对于半正定矩阵来说，相应的条件应改为所有的主子式非负。顺序主子式非负并不能推出矩阵是半正定的。

2、半正定矩阵

定义：设$A$是实对称矩阵。 如果对任意的实非零列矩阵$X$有$X^T * A * X \ge 0$，就称$A$为半正定矩阵。

3、$A\in M_n(K)$是半正定矩阵的充要条件是：$A$的所有主子式大于或等于零。

**参考：**

> 1.  [http://baike.baidu.com/view/686970.htm](http://baike.baidu.com/view/686970.htm)
> 2.  [http://baike.baidu.com/view/5925345.htm](http://baike.baidu.com/view/5925345.htm)
> 3.  [http://baike.baidu.com/view/826043.htm](http://baike.baidu.com/view/826043.htm)