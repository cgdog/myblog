---
title: leetCode 516. Longest Palindromic Subsequence
id: 823
categories:
  - algorithm
date: 2017-02-10 17:27:11
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[516\. Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/)

Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

**Example 1:**

Input:

    "bbbab"

    Output:

    `**4**`

    One possible longest palindromic subsequence is "bbbb".

    **Example 2:**
    Input:

    `"cbbd"`

    Output:

    `2`

One possible longest palindromic subsequence is "bb".

Solution 1: (Top bottom recursive method with memoization 62ms)



``` cpp
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        vector<vector<int>> memo(s.size(), vector<int>(s.size(), -1));
        return helper(0, s.size()-1, s, memo);
    }
    int helper(int i, int j, string &s, vector<vector<int>>& memo) {
        if (i > j) return 0;
        if (memo[i][j] != -1) {
            return memo[i][j];
        }
        if (i == j) {
            memo[i][j] = 1;
        } else if (s[i] == s[j]) {
            if (i +1 == j) {
                memo[i][j] = 2;
            } else {
                memo[i][j] = 2 + helper(i+1, j-1, s, memo);
            }
        } else {
            memo[i][j] = max(helper(i+1, j, s, memo), helper(i, j-1, s, memo));
        }
        return memo[i][j];
    }
};
```

Solution 2: DP solution (Bottom to up 79 ms.)



``` cpp
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int n = s.size();
        vector<vector<int>> dp(n, vector<int>(n, 0));
        for (int i = n-1; i >= 0; i--) {
            dp[i][i] = 1;
            for (int j = i + 1; j < n; j++) {
                if (s[i] == s[j]) {
                    dp[i][j] = dp[i+1][j-1] + 2;
                } else {
                    dp[i][j] = max(dp[i+1][j], dp[i][j-1]);
                }
            }
        }
        return dp[0][n-1];
    }
};
```

Reference: [https://discuss.leetcode.com/topic/78603/straight-forward-java-dp-solution](https://discuss.leetcode.com/topic/78603/straight-forward-java-dp-solution)