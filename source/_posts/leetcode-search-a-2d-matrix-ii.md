---
title: leetCode Search a 2D Matrix II
id: 388
categories:
  - algorithm
date: 2016-09-16 16:45:01
tags:
  - leetcode
---

[Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/)

Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.

Integers in each column are sorted in ascending from top to bottom.

For example,

Consider the following matrix:

[

&nbsp;&nbsp;&nbsp;&nbsp;[1,   4,  7, 11, 15],

&nbsp;&nbsp;&nbsp;&nbsp;[2,   5,  8, 12, 19],

&nbsp;&nbsp;&nbsp;&nbsp;[3,   6,  9, 16, 22],

&nbsp;&nbsp;&nbsp;&nbsp;[10, 13, 14, 17, 24],

&nbsp;&nbsp;&nbsp;&nbsp;[18, 21, 23, 26, 30]

]

Given target = 5, return true.

Given target = 20, return false.



``` cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int m = matrix.size();
        if (m < 1) {
            return false;
        }
        int n = matrix[0].size();

        int i = 0, j = n - 1;
        while (i >= 0 && i < m && j >= 0 && j < n) {
            if (matrix[i][j] == target) {
                return true;
            } else if(matrix[i][j] < target) {
                i++;
            } else {
                j--;
            }
        }
        return false;
    }
};
```

从矩阵右上角元素matrix[i][j]开始考虑，若target > matrix[i][j], 则第i行可以舍弃，即i++; 若target &lt; matrix[i][j], 则第j列元素可以舍弃，即j--; 若target == matrix[i][j]，则返回true。最后返回false，未找到target.