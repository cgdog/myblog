---
title: 115. Distinct Subsequences
id: 784
categories:
  - algorithm
date: 2017-01-06 16:01:18
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[115\. Distinct Subsequences](https://leetcode.com/problems/distinct-subsequences/)

Given a string S and a string T, count the number of distinct subsequences of T in S.

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ACE" is a subsequence of "ABCDE" while "AEC" is not).

Here is an example:

S = "rabbbit", T = "rabbit"

Return 3.


``` cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        vector<vector<int>> dp(t.size()+1, vector<int>(s.size()+1, 0));
        for (int i = 0; i < s.size(); i++) {
            dp[0][i] = 1;
        }
        for (int i = 1; i <= t.size(); i++) {
            for (int j = 1; j <= s.size(); j++) {
                if (t[i-1] == s[j-1]) {
                    dp[i][j] = dp[i][j-1] + dp[i-1][j-1];
                } else {
                    dp[i][j] = dp[i][j-1];
                }
            }
        }
        return dp[t.size()][s.size()];
    }
};
```

[https://discuss.leetcode.com/topic/9488/easy-to-understand-dp-in-java](https://discuss.leetcode.com/topic/9488/easy-to-understand-dp-in-java)