---
title: leetCode Find Peak Element
tags:
  - Binary Search
  - leetcode
id: 379
categories:
  - algorithm
date: 2016-09-16 11:05:06
---

[Find Peak Element](https://leetcode.com/problems/find-peak-element/)
A peak element is an element that is greater than its neighbors.

Given an input array where `num[i] ≠ num[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `num[-1] = num[n] = -∞`.

For example, in array `[1, 2, 3, 1]`, 3 is a peak element and your function should return the index number 2.

Note:

Your solution should be in logarithmic complexity.



``` cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {

        int low = 0, high = nums.size() - 1;
        while (low < high) {
            int mid = low + (high - low) / 2;
            int mid2 = mid + 1;
            if (nums[mid] < nums[mid2]) {
                low = mid2;
            } else {
                high = mid;
            }
        }
        return low;
    }
};
```

### how it works and why using binary searching on unsorted array is reasonable in this problem?

### Explanation:

Lets say you have a mid number at index x, nums[x]
if (num[x+1] > nums[x]), that means a peak element HAS to exist on the right half of that array, because (since every number is unique) 1\. the numbers keep increasing on the right side, and the peak will be the last element. 2\. the numbers stop increasing and there is a 'dip', or there exists somewhere a number such that nums[y] &lt; nums[y-1], which means number[x] is a peak element.

This same logic can be applied to the left hand side (nums[x] &lt; nums[x-1]).

> Reference:[https://discuss.leetcode.com/topic/5724/find-the-maximum-by-binary-search-recursion-and-iteration/24](https://discuss.leetcode.com/topic/5724/find-the-maximum-by-binary-search-recursion-and-iteration/24)