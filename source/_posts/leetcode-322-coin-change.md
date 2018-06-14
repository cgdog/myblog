---
title: leetcode 322. Coin Change
id: 810
categories:
  - algorithm
date: 2017-01-18 21:08:45
tags:
  - C++
  - Dynamic programming
  - leetcode
  - 背包
---

# [322\. Coin Change](https://leetcode.com/problems/coin-change/)

You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

**Example 1:**

coins = `[1, 2, 5]`, amount = `11`
return `3` (11 = 5 + 5 + 1)

**Example 2:**

coins = `[2]`, amount = `3`
return `-1`.

**Note:**

You may assume that you have an infinite number of each kind of coin.

DP solution:



``` cpp
    class Solution {
    public:
        int coinChange(vector&lt;int&gt;&amp; coins, int amount) {
            vector&lt;int&gt; dp(amount+1, amount+1);
            dp[0] = 0;
            for (int i = 1; i &lt;= amount; i++) {
                for (int j = 0; j &lt; coins.size(); j++) {
                    if (i &gt;= coins[j]) {
                        dp[i] = min(dp[i], dp[i-coins[j]]+1);
                    }
                }
            }
            return dp[amount] &gt; amount ? -1 : dp[amount];
        }
    };
```

Reference:

1\. [https://discuss.leetcode.com/topic/32475/c-o-n-amount-time-o-amount-space-dp-solution](https://discuss.leetcode.com/topic/32475/c-o-n-amount-time-o-amount-space-dp-solution)

2\. [https://discuss.leetcode.com/topic/32489/java-both-iterative-and-recursive-solutions-with-explanations](https://discuss.leetcode.com/topic/32489/java-both-iterative-and-recursive-solutions-with-explanations)