---
title: leetCode 72. Edit Distance
id: 788
categories:
  - algorithm
date: 2017-01-08 11:28:34
tags:
  - C++
  - Dynamic programming
  - leetcode
---

# [72\. Edit Distance](https://leetcode.com/problems/edit-distance/)

Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2\. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

a) Insert a character

b) Delete a character

c) Replace a character

DP Solution 1 with O(m*n)space.


``` cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.size();
        int n = word2.size();
        vector<vector<int>> dp(m+1, vector<int>(n+1, 0));
        for (int i = 1; i <=m; i++) {
            dp[i][0] = i;
        }
        for (int j = 1; j <=n; j++) {
            dp[0][j] = j;
        }
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1[i-1] == word2[j-1]) {
                    dp[i][j] = dp[i-1][j-1];
                } else {
                    dp[i][j] = min(dp[i-1][j-1]+1, min(dp[i][j-1]+1, dp[i-1][j]+1));
                }
            }
        }
        return dp[m][n];
    }
};
```

DP Solution 2 with O(m)space.


``` cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int m = word1.size();
        int n = word2.size();
        vector<int> dp(m+1, 0);
        for (int i = 1; i <=m; i++) {
            dp[i] = i;
        }
        for (int j = 1; j <= n; j++) {
            int pre = dp[0];
            dp[0] = j;
            for (int i = 1; i <= m; i++) {
                int tmp = dp[i];
                if (word1[i-1] == word2[j-1]) {
                    dp[i] = pre;
                } else {
                    dp[i] = min(pre+1, min(dp[i]+1, dp[i-1]+1));
                }
                pre = tmp;
            }
        }
        return dp[m];
    }
};
```

[https://discuss.leetcode.com/topic/17639/20ms-detailed-explained-c-solutions-o-n-space](https://discuss.leetcode.com/topic/17639/20ms-detailed-explained-c-solutions-o-n-space)