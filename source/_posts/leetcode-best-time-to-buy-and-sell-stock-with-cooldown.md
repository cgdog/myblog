---
title: Best Time to Buy and Sell Stock with Cooldown
id: 744
categories:
  - algorithm
date: 2016-12-16 16:15:53
tags:
  - Dynamic programming
  - leetcode
---

[Best Time to Buy and Sell Stock with Cooldown](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)
Example:



```
prices = [1, 2, 3, 0, 2]
maxProfit = 3
transactions = [buy, sell, cooldown, buy, sell]
```



``` cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int pre_buy, sell(0), buy(INT_MIN), pre_sell(0);
        for (int i = 0; i < prices.size(); i++) {
            pre_buy = buy;
            buy = max(pre_sell-prices[i], buy);
            pre_sell = sell;
            sell = max(pre_buy+prices[i], sell);
        }
        return sell;
    }
};
```

[https://discuss.leetcode.com/topic/30421/share-my-thinking-process](https://discuss.leetcode.com/topic/30421/share-my-thinking-process)

[https://discuss.leetcode.com/topic/30680/share-my-dp-solution-by-state-machine-thinking](https://discuss.leetcode.com/topic/30680/share-my-dp-solution-by-state-machine-thinking)