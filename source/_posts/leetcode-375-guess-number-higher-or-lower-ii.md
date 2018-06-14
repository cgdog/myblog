---
title: leetCode 375. Guess Number Higher or Lower II
id: 764
categories:
  - algorithm
date: 2016-12-17 23:27:33
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[375&#46; Guess Number Higher or Lower II](https://leetcode.com/problems/guess-number-higher-or-lower-ii/)

We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number I picked is higher or lower.

However, when you guess a particular number x, and you guess wrong, you pay $x. You win the game when you guess the number I picked.

Example:

    n = 10, I pick 8.

    First round:  You guess 5, I tell you that it's higher. You pay $5.
    Second round: You guess 7, I tell you that it's higher. You pay $7.
    Third round:  You guess 9, I tell you that it's lower. You pay $9.

    Game over. 8 is the number I picked.

    You end up paying $5 + $7 + $9 = $21.

Given a particular n ≥ 1, find out how much money you need to have to guarantee a win.

**Hint:**

1&#46;The best strategy to play the game is to minimize the maximum loss you could possibly face. Another strategy is to minimize the expected loss. Here, we are interested in the first scenario.

2&#46;Take a small example (n = 3). What do you end up paying in the worst case?

3&#46;Check out [this article](https://en.wikipedia.org/wiki/Minimax) if you're still stuck.

4&#46;The purely recursive implementation of minimax would be worthless for even a small n. You MUST use dynamic programming.

5&#46;As a follow-up, how would you modify your code to solve the problem of minimizing the expected loss, instead of the worst-case loss?

DP solution:



``` cpp
class Solution {
public:
    int DP(vector&lt;vector&lt;int>>& dp, int s, int t) {
        if (s >= t) return 0;
        if (dp[s][t] != 0) return dp[s][t];
        int res = INT_MAX;
        for (int x = s; x &lt;= t; x++) {
            int tmp = x + max(DP(dp, s, x-1), DP(dp, x+1, t));
            res = min(res, tmp);
        }
        dp[s][t] = res;
        return res;
    }
    int getMoneyAmount(int n) {
        vector&lt;vector&lt;int>> dp(n+1, vector&lt;int>(n+1, 0));
        return DP(dp, 1, n);
    }
};
```

DP bottom to up:



``` cpp
class Solution {
public:

    int getMoneyAmount(int n) {
        vector&lt;vector&lt;int>> dp(n+1, vector&lt;int>(n+1, 0));
        for (int j = 2; j &lt;=n; j++) {
            for (int i = j-1; i > 0; i--) {
                int globalMin = INT_MAX;
                for (int k=i+1; k &lt; j; k++) {
                    int localMax = k + max(dp[i][k-1], dp[k+1][j]);
                    globalMin = min(localMax, globalMin);
                }
                dp[i][j] = i+1==j? i : globalMin;
            }
        }
        return dp[1][n];
    }
};
```

Reference:[https://discuss.leetcode.com/topic/51353/simple-dp-solution-with-explanation](https://discuss.leetcode.com/topic/51353/simple-dp-solution-with-explanation)