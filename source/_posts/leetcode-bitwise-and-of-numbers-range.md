---
title: leetCode Bitwise AND of Numbers Range
tags:
  - Bit manipulation
  - leetcode
id: 434
categories:
  - algorithm
date: 2016-09-25 10:42:57
---

[Bitwise AND of Numbers Range](https://leetcode.com/problems/bitwise-and-of-numbers-range/)

Given a range [m, n] where 0 &lt;= m &lt;= n &lt;= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

For example, given the range [5, 7], you should return 4.



``` cpp
// 35 ms
class Solution {
public:
    int rangeBitwiseAnd(int m, int n) {
      int moveFactor = 1;
        while(m != n){
            m >>= 1;
            n >>= 1;
            moveFactor <<= 1;
        }
        return m * moveFactor;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/12133/bit-operation-solution-java](https://discuss.leetcode.com/topic/12133/bit-operation-solution-java)



``` cpp
// 42 ms
class Solution {
public:
    int rangeBitwiseAnd(int m, int n) {
      while (n > m) n &= (n-1);
      return n;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/12133/bit-operation-solution-java/10](https://discuss.leetcode.com/topic/12133/bit-operation-solution-java/10)