---
title: 'leetcode: Sum of Two Integers'
id: 317
categories:
  - algorithm
date: 2016-07-14 11:39:29
tags:
  - leetcode
---

Calculate the sum of two integers a and b, but you are not allowed to use the operator + and -.

Example: Given a = 1 and b = 2, return 3.



``` cpp
class Solution {
public:
    int getSum(int a, int b) {
        int one;
        int two;
        do {
            one=a ^ b;
            two=(a & b)<<1;
            a=one;
            b=two;

        } while(two!=0);

        return one;
    }
};
```

> 参考：忘记了网址了。。。