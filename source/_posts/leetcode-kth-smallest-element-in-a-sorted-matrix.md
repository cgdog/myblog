---
title: leetcode Kth Smallest Element in a Sorted Matrix
tags:
  - Binary Search
  - leetcode
id: 369
categories:
  - algorithm
date: 2016-09-14 17:14:35
---

[Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)

Given a n x n matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

Example:
```
matrix = [ [ 1, 5, 9], [10, 11, 13], [12, 13, 15] ], k = 8,

return 13\. Note: You may assume k is always valid, 1 ≤ k ≤ n2.```



``` cpp
class Solution {
public:
    int kthSmallest(vector<vector<int>>& matrix, int k) {
        int n = matrix.size();
        int left = matrix[0][0];
        int right = matrix[n-1][n-1];
        while (left < right) {
            int mid = left + (right - left) / 2;
            int count = 0;
            for (int i = 0; i < n; i++) {
                count += upper_bound(matrix[i].begin(), matrix[i].end(), mid) - matrix[i].begin();
            }

            if (count < k) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/52865/my-solution-using-binary-search-in-c/52](https://discuss.leetcode.com/topic/52865/my-solution-using-binary-search-in-c/52)