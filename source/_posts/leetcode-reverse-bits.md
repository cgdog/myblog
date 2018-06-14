---
title: 'leetcode: Reverse Bits'
id: 321
categories:
  - algorithm
date: 2016-07-14 13:28:25
tags:
  - leetcode
mathjax: true
---


Reverse bits of a given 32 bits unsigned integer.

For example, given input 43261596 (represented in binary as 00000010100101000001111010011100), return 964176192 (represented in binary as 00111001011110000010100101000000).

Follow up:

If this function is called many times, how would you optimize it?



``` cpp
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        uint32_t res = 0;
        for (int i = 0; i < 32; i++) {
            res |= ((n>>i)&1) << (31-i);
        }
        return res;
    } 
};
```

> 参考：[http://www.cnblogs.com/grandyang/p/4321355.html](http://www.cnblogs.com/grandyang/p/4321355.html)