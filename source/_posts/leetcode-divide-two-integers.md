---
title: 'leetcode: Divide Two Integers'
id: 324
categories:
  - algorithm
date: 2016-07-14 19:44:12
tags:
  - leetcode
---


Divide two integers without using multiplication, division and mod operator.

If it is overflow, return MAX_INT.

C++实现:



``` cpp
class Solution {
public:
    int divide(int dividend, int divisor) {
        if (divisor==INT_MIN) {
            if (dividend==INT_MIN) {
                return 1;
            }
            return 0;
        }

        if (dividend == INT_MIN && divisor == -1) {// avoid overflow : dividend = -2147483648, divisor = -1
            return INT_MAX;
        }

        bool isNeg = (dividend < 0 && divisor > 0) || (dividend > 0 && divisor < 0);
        int res = 0;

        divisor = divisor < 0? -divisor : divisor;

        if (dividend == INT_MIN) {

            res++;
            dividend += divisor;
        }

        dividend = dividend < 0? -dividend : dividend;

        int digit = 0;
        while (divisor <= (dividend >> 1)) {
            divisor <<= 1;
            digit++;
        }

        while (digit >= 0) {
            if (dividend >= divisor) {
                dividend -= divisor;

                res += 1<<digit;
            }
            divisor >>= 1;
            digit--;
        }

        res = isNeg? -res :res;
        return res;
    }
};
```

> 参考：[http://www.tuicool.com/articles/FNrUvyE](http://www.tuicool.com/articles/FNrUvyE)