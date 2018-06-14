---
title: Backpack 0-1背包空间优化
id: 124
categories:
  - algorithm
date: 2016-05-16 17:04:09
tags:
  - 背包
---

题目见lintcode上的[Backpack](http://www.lintcode.com/en/problem/backpack/)，0-1背包。

若是简单地用二维数组存储状态，对于一些测试数据会出现超出内存限制。

可以，改用一维数组存储状态。

代码如下：

```
class Solution {
public:
    /**
     * @param m: An integer m denotes the size of a backpack
     * @param A: Given n items with size A[i]
     * @return: The maximum size
     */
    int backPack(int m, vector&lt;int> A) {
       // write your code here
       vector&lt;int> dp(m+1, 0);

        for (int i = 1; i &lt;= A.size(); i++)
        {
            for (int j = m; j >= A[i-1]; j--)
            {
                int tmp = dp[j-A[i-1]]+A[i-1];
                dp[j] = (dp[j] >= tmp? dp[j] : tmp);
            }
        }

        return dp[m];
    }
};
```

其中的关键是内层的for循环要逆序进行。

> 原因是如果将内层for循环顺序由逆序改为顺序的话，就不是01背包了，就变成完全背包了。
> 
>   具体参考[http://blog.csdn.net/fobdddf/article/details/19479217](http://blog.csdn.net/fobdddf/article/details/19479217)
> 
>   和[http://www.cnblogs.com/fly1988happy/archive/2011/12/13/2285377.html](http://www.cnblogs.com/fly1988happy/archive/2011/12/13/2285377.html)
>   及[http://www.cnblogs.com/fly1988happy/archive/2011/12/13/2285377.html](http://www.cnblogs.com/fly1988happy/archive/2011/12/13/2285377.html)