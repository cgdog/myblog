---
title: leetcode 304. Range Sum Query 2D - Immutable
id: 812
categories:
  - algorithm
date: 2017-01-19 11:46:46
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[304\. Range Sum Query 2D - Immutable](https://leetcode.com/problems/range-sum-query-2d-immutable/)

Given a 2D matrix matrix, find the sum of the elements inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).

![Range Sum Query 2D](https://leetcode.com/static/images/courses/range_sum_query_2d.png)

The above rectangle (with the red border) is defined by (row1, col1) = (2, 1) and (row2, col2) = (4, 3), which contains sum = 8.

Example:



``` cpp
Given matrix = [
  [3, 0, 1, 4, 2],
  [5, 6, 3, 2, 1],
  [1, 2, 0, 1, 5],
  [4, 1, 0, 1, 7],
  [1, 0, 3, 0, 5]
]

sumRegion(2, 1, 4, 3) -> 8
sumRegion(1, 1, 2, 2) -> 11
sumRegion(1, 2, 2, 4) -> 12
```
**Note:**

1\. You may assume that the matrix does not change.

2\. There are many calls to sumRegion function.

3\. You may assume that row1 ≤ row2 and col1 ≤ col2.



``` cpp
    class NumMatrix {
    public:
        vector&lt;vector&lt;int&gt;&gt; dp;
        NumMatrix(vector&lt;vector&lt;int&gt;&gt; &amp;matrix) {
            if (!matrix.empty()) {
                dp.resize(matrix.size()+1, vector&lt;int&gt;(matrix[0].size()+1, 0));
                for (int i = 1; i &lt;= matrix.size(); i++) {
                    for (int j = 1; j &lt;= matrix[0].size(); j++) {
                       dp[i][j] = dp[i-1][j] + dp[i][j-1] - dp[i-1][j-1] + matrix[i-1][j-1];
                    }
                }
            }
        }

        int sumRegion(int row1, int col1, int row2, int col2) {
            if (dp.empty()) return 0;
            return dp[row2+1][col2+1] - dp[row1][col2+1] - dp[row2+1][col1] + dp[row1][col1];
        }
    };

    // Your NumMatrix object will be instantiated and called as such:
    // NumMatrix numMatrix(matrix);
    // numMatrix.sumRegion(0, 1, 2, 3);
    // numMatrix.sumRegion(1, 2, 3, 4);
```
Reference:[https://discuss.leetcode.com/topic/29536/clean-c-solution-and-explaination-o-mn-space-with-o-1-time](https://discuss.leetcode.com/topic/29536/clean-c-solution-and-explaination-o-mn-space-with-o-1-time)