---
title: Can I Win
id: 799
categories:
  - algorithm
date: 2017-01-18 11:42:47
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[464\. Can I Win](https://leetcode.com/problems/can-i-win/)

In the "100 game," two players take turns adding, to a running total, any integer from 1..10\. The player who first causes the running total to reach or exceed 100 wins.

What if we change the game so that players cannot re-use integers?

For example, two players might take turns drawing from a common pool of numbers of 1..15 without replacement until they reach a total >= 100.

Given an integer maxChoosableInteger and another integer desiredTotal, determine if the first player to move can force a win, assuming both players play optimally.

You can always assume that maxChoosableInteger will not be larger than 20 and desiredTotal will not be larger than 300.

Example

    Input:
    maxChoosableInteger = 10
    desiredTotal = 11

    Output:
    false

    Explanation:
    No matter which integer the first player choose, the first player will lose.
    The first player can choose an integer from 1 up to 10.
    If the first player choose 1, the second player can only choose integers from 2 up to 10.
    The second player will win by choosing 10 and get a total = 11, which is &gt;= desiredTotal.
    Same with other integers chosen by the first player, the second player will always win.



``` cpp
class Solution {
public:
    bool helper(int desiredTotal, unordered_map<int, bool> &dp, int available, int maxChoosableInteger) {
        if (dp.find(available) != dp.end()) {
            return dp[available];
        }
        for (int i = maxChoosableInteger; i > 0; i--) {
            int bit = (1 << i); 
            if (available & bit) {
                if (i >= desiredTotal) {
                    dp[available] = true;
                    return true;
                }
                bool oppo = helper(desiredTotal-i, dp, available ^ bit, maxChoosableInteger);
                dp[available ^ bit] = oppo;
                if (!oppo) {
                    return true;
                }
            }

        }
        return false;
    }
    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        if (desiredTotal == 0) return true;
        if ((1+maxChoosableInteger)*maxChoosableInteger/2 < desiredTotal) return false;

        unordered_map<int, bool> dp;
        int available = 0;
        for (int i = 0; i <= maxChoosableInteger; i++) {
            available |= (1 << i);
        }
        return helper(desiredTotal, dp, available, maxChoosableInteger);
    }
};
```

Reference:

[https://discuss.leetcode.com/topic/68835/dp-solution-in-c-with-comments](https://discuss.leetcode.com/topic/68835/dp-solution-in-c-with-comments)

[https://discuss.leetcode.com/topic/68896/java-solution-using-hashmap-with-detailed-explanation](https://discuss.leetcode.com/topic/68896/java-solution-using-hashmap-with-detailed-explanation)