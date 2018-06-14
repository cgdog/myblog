---
title: Best Time to Buy and Sell Stock III
id: 748
categories:
  - algorithm
date: 2016-12-16 17:40:57
tags:
  - Dynamic programming
---

[Best Time to Buy and Sell Stock III](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)

Say you have an array for which the $i_{th}$ element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

**Note**:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

My naive idea (which is Time Limit Exceeded):



``` cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int prof = 0;
        for (int i = 1; i < prices.size(); i++) {
            int prof1 = 0, prof2 = 0, min_price = INT_MAX;
            for (int j = 0; j <= i; j++) {
                min_price = min(min_price, prices[j]);
                prof1 = max(prof1, prices[j]-min_price);
            }
            min_price = INT_MAX;
            for (int j = i+1; j < prices.size(); j++) {
                min_price = min(min_price, prices[j]);
                prof2 = max(prof2, prices[j]-min_price);
            }
            prof = max(prof, prof1+prof2);
        }
        return prof;
    }
};
```

AC solution:


``` cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int buy1 = INT_MIN, sell1 = 0, buy2 = INT_MIN, sell2 = 0;
        for (int price : prices) {
            sell2 = max(sell2, buy2+price);
            buy2 = max(buy2, sell1-price);
            sell1 = max(sell1, buy1+price);
            buy1 = max(buy1, -price);
        }
        return sell2;
    }
};
```

[https://discuss.leetcode.com/topic/5934/is-it-best-solution-with-o-n-o-1](https://discuss.leetcode.com/topic/5934/is-it-best-solution-with-o-n-o-1)

[https://discuss.leetcode.com/topic/19750/my-c-solution-o-n-time-o-1-space-8ms](https://discuss.leetcode.com/topic/19750/my-c-solution-o-n-time-o-1-space-8ms)