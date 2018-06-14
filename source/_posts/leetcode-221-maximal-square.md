---
title: leetcode 221. Maximal Square
id: 806
categories:
  - algorithm
date: 2017-01-18 19:55:07
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[221\. Maximal Square](https://leetcode.com/problems/maximal-square/)

Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

For example, given the following matrix:

    1 0 1 0 0
    1 0 1 1 1
    1 1 1 1 1
    1 0 0 1 0

Return 4.
Accepted Naive solution (O(1) space):



``` cpp
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        int m = matrix.size();
        if (m == 0) return 0;
        int n = matrix[0].size();
        int min_mn = min(m, n);
        int area = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (matrix[i][j] == '0') continue;
                area = max(1, area);
                for (int k = 1; k+i < m && k+j < n; k++) {
                    bool flag = true;
                    for (int ii = i; ii <= k+i; ii++) {
                        for (int jj = j; jj <= k+j; jj++) {
                            if (matrix[ii][jj] == '0') {
                                flag = false;
                                break;
                            }
                        }
                        if (!flag) break;
                    }

                    if (!flag) {
                        area = max(area, k*k);
                        break;
                    } else {
                        area = max(area, (k+1)*(k+1));
                    }
                }
            }
        }
        return area;
    }
};
```

DP solution (O(m) space):



``` cpp
class Solution {
public:
    int maximalSquare(vector<vector<char>>& matrix) {
        if (matrix.empty()) return 0;
        int m = matrix.size();
        int n = matrix[0].size();
        vector<int> dp(m+1, 0);
        int pre = 0, side = 0;
        for (int j = 0; j < n; j++) {
            for (int i = 1; i <= m; i++) {
                int tmp = dp[i];
                if (matrix[i-1][j] == '1') {
                    dp[i] = min(dp[i], min(dp[i-1], pre))+1;
                    side = max(side, dp[i]);
                } else {
                    dp[i] = 0;
                }
                pre = tmp;
            }
        }
        return side * side;
    }
};
```

Reference:[https://discuss.leetcode.com/topic/15328/easy-dp-solution-in-c-with-detailed-explanations-8ms-o-n-2-time-and-o-n-space](https://discuss.leetcode.com/topic/15328/easy-dp-solution-in-c-with-detailed-explanations-8ms-o-n-2-time-and-o-n-space)