---
title: leetcode 303. Range Sum Query - Immutable
id: 808
categories:
  - algorithm
date: 2017-01-18 20:14:49
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[303\. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/)

Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

**Example:**


``` cpp
    Given nums = [-2, 0, 3, -5, 2, -1]

    sumRange(0, 2) -> 1
    sumRange(2, 5) -> -1
    sumRange(0, 5) -> -3
```

    **Note:**
    You may assume that the array does not change.
    There are many calls to sumRange function.

    Simple DP solution:


``` cpp
class NumArray {
    public:
        vector&lt;int&gt; dp;
        bool flag = false;
        NumArray(vector&lt;int&gt; &amp;nums) {
            if (nums.size() == 0) flag = true;
            if (nums.size() &gt; 0) {
                dp.resize(nums.size(), 0);
                dp[0] = nums[0];
                for (int i = 1; i &lt; nums.size(); i++) {
                    dp[i] = dp[i-1] + nums[i];
                }
            }
        }

        int sumRange(int i, int j) {
            if (flag) return 0;
            if (i == 0)
                return dp[j];
            else
                return dp[j] - dp[i-1];
        }
    };

    // Your NumArray object will be instantiated and called as such:
    // NumArray numArray(nums);
    // numArray.sumRange(0, 1);
    // numArray.sumRange(1, 2);
```
    