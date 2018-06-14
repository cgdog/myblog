---
title: Best Time to Buy and Sell Stock IV
id: 752
categories:
  - algorithm
date: 2016-12-16 18:10:37
tags:
  - Dynamic programming
  - leetcode
---

[Best Time to Buy and Sell Stock IV](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most k transactions.

**Note:**

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).


``` cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        if (k == 0) return 0;
        if (k > prices.size()) {// to avoid Time Limit Exceeded....
            int prof = 0;
            for (int i = 1; i < prices.size(); i++) {
                if (prices[i] > prices[i-1]) {
                    prof += prices[i]-prices[i-1];
                }
            }
            return prof;
        }
        vector<vector<int>> dp(k, vector<int>(2));
        for (int i = 0; i < k; i++) {
            dp[i][0] = INT_MIN;
            dp[i][1] = 0;
        }

        for (int price : prices) {
            for (int i = k-1; i>=0; i--) {
                dp[i][1] = max(dp[i][1], dp[i][0]+price);
                if (i == 0)
                    dp[i][0] = max(dp[i][0], -price);
                else
                    dp[i][0] = max(dp[i][0], dp[i-1][1]-price);
            }
        }
        return dp.back()[1];
    }
};
```

My solution use O(k),in fact, O(2k) space.

Solutions below use O(kn) space.

[https://discuss.leetcode.com/topic/26169/clean-java-dp-solution-with-comment](https://discuss.leetcode.com/topic/26169/clean-java-dp-solution-with-comment)

[https://discuss.leetcode.com/topic/8984/a-concise-dp-solution-in-java](https://discuss.leetcode.com/topic/8984/a-concise-dp-solution-in-java)