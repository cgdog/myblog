---
title: Solve linear least squares systems using Eigen
tags:
  - Eigen
  - math
id: 666
categories:
  - algorithm
date: 2016-11-07 22:18:04
---

# 使用eigen解线性最小二乘系统(方程组)

> Reference:[https://eigen.tuxfamily.org/dox-devel/group__LeastSquares.html](https://eigen.tuxfamily.org/dox-devel/group__LeastSquares.html)

An overdetermined system of equations, say Ax = b, has no solutions. In this case, it makes sense to search for the vector x which is closest to being a solution, in the sense that the difference Ax - b is as small as possible. This x is called the least square solution (if the Euclidean norm is used).

一个超定方程组，比如`Ax=b`，没有解。在这种情况下，寻找最接近解的向量`x`就非常有意义了，即使得`Ax-b`接近0。则`x`被称为最小二乘解(若使用欧几里得范式的情况下)。

The three methods discussed on this page are the SVD decomposition, the QR decomposition and normal equations. Of these, the SVD decomposition is generally the most accurate but the slowest, normal equations is the fastest but least accurate, and the QR decomposition is in between.

本文讨论了三种解法：**SVD分解** （最精确但最慢）、**QR分解** （精确率和速度在中间）、**标准方程组解法** （最快但最不精确）。

例子如下：



``` cpp
#include <iostream>
#include <Eigen/Dense>
using namespace std;
using namespace Eigen;
int main()
{
    // https://eigen.tuxfamily.org/dox-devel/group__LeastSquares.html
    MatrixXf A = MatrixXf::Random(3, 2);
    cout << "Here is the matrix A:\n" << A << endl;
    VectorXf b = VectorXf::Random(3);
    cout << "Here is the right hand side b:\n" << b << endl;
    cout << "The least-squares solution using the SVD decomposition is:\n"
        << A.jacobiSvd(ComputeThinU | ComputeThinV).solve(b) << endl;

    cout << "\nThe solution using the QR decomposition is:\n"
        << A.colPivHouseholderQr().solve(b) << endl;

    cout << "\nThe solution using normal equations is:\n"
        << (A.transpose() * A).ldlt().solve(A.transpose() * b) << endl;
    return 0;
}
```

输出:

```Here is the matrix A:
 -0.997497   0.617481
  0.127171   0.170019
 -0.613392 -0.0402539
Here is the right hand side b:
-0.299417
 0.791925
  0.64568
The least-squares solution using the SVD decomposition is:
-0.170347
-0.420746

The solution using the QR decomposition is:
-0.170348
-0.420747

The solution using normal equations is:
-0.170348
-0.420747
请按任意键继续. . .
```