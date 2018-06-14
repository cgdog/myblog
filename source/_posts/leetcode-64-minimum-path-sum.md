---
title: leetCode 64. Minimum Path Sum
id: 762
categories:
  - algorithm
date: 2016-12-17 20:54:56
tags:
  - Dynamic programming
  - leetcode
---

[64\. Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/)

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**Note:** You can only move either down or right at any point in time.

Naive DP solution without optimization, O(mn) space:


``` cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        if (m < 1) return 0;
        int n = grid[0].size();
        vector<vector<int>> dp(m, vector<int>(n, grid[0][0]));
        for (int i = 1; i < n; i++) {
            dp[0][i] = grid[0][i] + dp[0][i-1];
        }
        for (int i = 1; i < m; i++) {
            dp[i][0] = grid[i][0] + dp[i-1][0];
        }
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + grid[i][j];
            }
        }
        return dp[m-1][n-1];
    }
};
```

Below is optimized solution O(m) space.



``` cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        if (m < 1) return 0;
        int n = grid[0].size();

        vector<int> dp(m, grid[0][0]);
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (i==0) {
                    dp[j] = dp[j-1] + grid[j][i];
                } else if (j == 0) {
                    dp[j] = dp[j] + grid[j][i];
                } else {
                    dp[j] = min(dp[j], dp[j-1]) + grid[j][i];
                }
            }
        }
        return dp[m-1];
    }
};
```

Reference:[https://discuss.leetcode.com/topic/15269/10-lines-28ms-o-n-space-dp-solution-in-c-with-explanations](https://discuss.leetcode.com/topic/15269/10-lines-28ms-o-n-space-dp-solution-in-c-with-explanations)