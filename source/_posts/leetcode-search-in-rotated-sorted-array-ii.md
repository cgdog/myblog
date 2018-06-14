---
title: leetCode Search in Rotated Sorted Array II
id: 376
categories:
  - algorithm
date: 2016-09-15 23:54:00
tags:
  - leetcode
---

[Search in Rotated Sorted Array II](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)

Follow up for "[Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/)": What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.



``` cpp
class Solution {
public:
    bool search(vector<int>& nums, int target) {
        int i = 0, j = nums.size() - 1;
        while (i <= j) {
            int m = i + (j - i) / 2;
            if (nums[m] == target) {
                return true;
            }
            if (nums[i] < nums[m]) {
                if (nums[i] <= target && nums[m] > target) {
                    j = m - 1;
                } else {
                    i = m + 1;
                }
            } else if (nums[i] > nums[m]) {
                if (nums[m] < target && nums[j] >= target) {
                    i = m + 1;
                } else {
                    j = m - 1;
                }
            } else {
                i++;
            }
        }

        return false;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/310/when-there-are-duplicates-the-worst-case-is-o-n-could-we-do-better/3](https://discuss.leetcode.com/topic/310/when-there-are-duplicates-the-worst-case-is-o-n-could-we-do-better/3) [https://discuss.leetcode.com/topic/8087/c-concise-log-n-solution](https://discuss.leetcode.com/topic/8087/c-concise-log-n-solution)