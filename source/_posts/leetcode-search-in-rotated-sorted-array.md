---
title: leetCode Search in Rotated Sorted Array
tags:
  - Binary Search
  - leetcode
id: 372
categories:
  - algorithm
date: 2016-09-15 10:14:32
---

[Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.



``` cpp
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int i = 0, j = nums.size() - 1;
        while (i < j) {
            int mid = (j + i) / 2;
            if (nums[mid] > nums[j]) {
                i = mid + 1;
            } else {
                j = mid;
            }
        }

        int step = i;
        i = 0;
        j = nums.size() - 1;
        while (i <= j) {// 此处用 i < j，循环内部else用j = mid的话，对于[1] 1 测试用例不通过。
            int mid = (j + i) / 2;
            int realMid = (mid + step) % nums.size();
            if (nums[realMid] == target) {
                return realMid;
            } else if (nums[realMid] < target) {
                i = mid + 1;
            } else {
                j = mid - 1;
            }
        }

        return -1;
    }
};
```

> 参考：[https://discuss.leetcode.com/topic/3538/concise-o-log-n-binary-search-solution/4](https://discuss.leetcode.com/topic/3538/concise-o-log-n-binary-search-solution/4)