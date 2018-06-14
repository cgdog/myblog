---
title: Unique Paths
id: 756
categories:
  - algorithm
date: 2016-12-16 23:42:47
tags:
  - Dynamic programming
  - leetcode
---

[Unique Paths](https://leetcode.com/problems/unique-paths/)

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

![](http://leetcode.com/wp-content/uploads/2014/12/robot_maze.png)

Above is a 3 x 7 grid. How many possible unique paths are there?

Note: m and n will be at most 100.



``` cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        if (m > n) { // to cost low extra space.
            uniquePaths(n, m);
        }
        vector<int> dp(m, 1);
        for (int i = 1; i < n; i++) {
            for (int j = 1; j < m; j++) {
                dp[j] += dp[j-1];
            }
        }
        return dp[m-1];
    }
};
```

[https://discuss.leetcode.com/topic/15265/0ms-5-lines-dp-solution-in-c-with-explanations](https://discuss.leetcode.com/topic/15265/0ms-5-lines-dp-solution-in-c-with-explanations)