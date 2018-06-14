---
title: leetCode Single Number III
tags:
  - Bit manipulation
  - leetcode
id: 419
categories:
  - algorithm
date: 2016-09-23 20:05:49
---

[Single Number III](https://leetcode.com/problems/single-number-iii/)

Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

For example:

Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].

Note:

The order of the result is not important. So in the above example, [5, 3] is also correct.

Your algorithm should run in linear runtime complexity. Could you implement it using only constant space complexity?



``` cpp
class Solution {
public:
    vector<int> singleNumber(vector<int>& nums) {
        int m = 0;
        vector<int> res(2, 0);
        for (int i = 0; i < nums.size(); i++) {
            m ^= nums[i];
        }
        m &= -m;
        for (int i = 0; i < nums.size(); i++) {
            if ((nums[i] & m) != 0) {
                res[0] ^= nums[i];
            } else {
                res[1] ^= nums[i];
            }
        }
        return res;
    }
};
```

``int m = 3;```

则 m &amp; (-m) 的值为：把m的二进制中最右边的1之前的所有位置为0。也就是得到m的右边为1的二进制位。

> Reference:[https://leetcode.com/problems/single-number-iii/](https://leetcode.com/problems/single-number-iii/)