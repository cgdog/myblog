---
title: Maximum Subarray
id: 754
categories:
  - algorithm
date: 2016-12-16 18:20:30
tags:
  - Dynamic programming
---

[Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [-2,1,-3,4,-1,2,1,-5,4],

the contiguous subarray [4,-1,2,1] has the largest sum = 6.



``` cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if (nums.size() < 0) return 0;
        int maxSoFar = nums[0], maxEndingHere = nums[0];
        for (int i = 1; i < nums.size(); i++) {
            maxEndingHere = max(nums[i], maxEndingHere+nums[i]);
            maxSoFar = max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    }
};
```

[https://en.wikipedia.org/wiki/Maximum_subarray_problem](https://en.wikipedia.org/wiki/Maximum_subarray_problem)

[https://discuss.leetcode.com/topic/4175/share-my-solutions-both-greedy-and-divide-and-conquer](https://discuss.leetcode.com/topic/4175/share-my-solutions-both-greedy-and-divide-and-conquer)