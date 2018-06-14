---
title: leetCode 410. Split Array Largest Sum
id: 780
categories:
  - algorithm
date: 2017-01-05 17:06:07
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[410\. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)

Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.

**Note:**

Given m satisfies the following constraint: 1 ≤ m ≤ length(nums) ≤ 14,000.

Examples:


```
    Input:
    nums = [7,2,5,10,8]
    m = 2

    Output:
    18
```
    Explanation:
    There are four ways to split nums into two subarrays.
    The best way is to split it into [7,2,5] and [10,8],
    where the largest sum among the two subarrays is only 18.



``` cpp
    class Solution {
    public:
        bool valid(int target, vector<int>& nums, int m) {
            int count = 1;
            int total = 0;
            for (int num : nums) {
                total += num;
                if (total > target) {
                    total = num;
                    count++;
                    if (count > m) {
                        return false;
                    }
                }
            }
            return true;
        }
        int splitArray(vector<int>& nums, int m) {
            int max_val = 0, sum = 0;
            for (int num : nums) {
                max_val = max(max_val, num);
                sum += num;
            }
            if (m==1) return sum;
            int left = max_val, right = sum;
            while (left <= right) {
                int mid = left + (right - left) / 2;
                if (valid(mid, nums, m)) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            }
            return left;
        }
    };
```
[https://discuss.leetcode.com/topic/61324/clear-explanation-8ms-binary-search-java](https://discuss.leetcode.com/topic/61324/clear-explanation-8ms-binary-search-java)