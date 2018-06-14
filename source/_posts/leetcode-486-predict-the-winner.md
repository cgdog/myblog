---
title: leetCode 486. Predict the Winner
id: 821
categories:
  - algorithm
date: 2017-02-10 11:59:59
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[486\. Predict the Winner](https://leetcode.com/problems/predict-the-winner/)

Given an array of scores that are non-negative integers. Player 1 picks one of the numbers from either end of the array followed by the player 2 and then player 1 and so on. Each time a player picks a number, that number will not be available for the next player. This continues until all the scores have been chosen. The player with the maximum score wins.

Given an array of scores, predict whether player 1 is the winner. You can assume each player plays to maximize his score.

**Example 1:**
Input: [1, 5, 2]

    Output: False
    Explanation: Initially, player 1 can choose between 1 and 2\. 
    If he chooses 2 (or 1), then player 2 can choose from 1 (or 2) and 5\. If player 2 chooses 5, then player 1 will be left with 1 (or 2). 
    So, final score of player 1 is 1 + 2 = 3, and player 2 is 5\. 
    Hence, player 1 will never be the winner and you need to return False.
    

    **Example 2:**

    `Input: [1, 5, 233, 7]
    Output: True
    Explanation: Player 1 first chooses 1\. Then player 2 have to choose between 5 and 7\. No matter which number player 2 choose, player 1 can choose 233.
    Finally, player 1 has more score (234) than player 2 (12), so you need to return True representing player1 can win.

**Note:**

1\. 1 <= length of the array <= 20.

2\. Any scores in the given array are non-negative integers and will not exceed 10,000,000.

3\. If the scores of both players are equal, then player 1 is still the winner.

Recursion Solution (89 ms):




``` cpp
class Solution {
public:
    bool PredictTheWinner(vector<int>& nums) {
        return helper(nums, 0, nums.size()-1) >= 0;
    }
    int helper(vector<int>& nums, int s, int e) {
        return (s==e) ? nums[s] : max(nums[s]-helper(nums, s + 1, e), nums[e] - helper(nums, s, e-1));
    }
};
```

Recursion Solution (3ms):



``` cpp
class Solution {
public:
    bool PredictTheWinner(vector<int>& nums) {
        vector<vector<int>> cach(nums.size(), vector<int>(nums.size(), -1));
        return helper(nums, 0, nums.size()-1, cach) >= 0;
    }
    int helper(vector<int>& nums, int s, int e, vector<vector<int>> &cach) {
        if (cach[s][e] == -1) {
            cach[s][e] = (s==e) ? nums[s] : max(nums[s]-helper(nums, s + 1, e, cach), nums[e] - helper(nums, s, e-1, cach));
        }
        return cach[s][e];
    }
};
```

Reference: [https://discuss.leetcode.com/topic/76312/java-1-line-recursion-solution](https://discuss.leetcode.com/topic/76312/java-1-line-recursion-solution)

DP Solution 1:



``` cpp
class Solution {
public:
    bool PredictTheWinner(vector<int>& nums) {
        if (nums.size() % 2 == 0) return true;
        int n = nums.size();
        vector<vector<int>> dp(n, vector<int>(n, -1));
        int firstBest = helper(nums, dp, 0, n-1);
        return 2 * firstBest >= accumulate(nums.begin(), nums.end(), 0);
    }
    int helper(vector<int>& nums, vector<vector<int>> &dp, int i, int j) {
        if (i > j) return 0;
        if (dp[i][j] != -1) return dp[i][j];
        int a = nums[i] + min(helper(nums, dp, i+1, j-1), helper(nums, dp, i+2, j));
        int b = nums[j] + min(helper(nums, dp, i+1, j-1), helper(nums, dp, i, j-2));
        dp[i][j] = max(a, b);
        return dp[i][j];
    }
};
```

Reference: [https://discuss.leetcode.com/topic/76323/dp-o-n-2-mit-ocw-solution-explanation](https://discuss.leetcode.com/topic/76323/dp-o-n-2-mit-ocw-solution-explanation)

DP Solution 2:



``` cpp
class Solution {
public:
    bool PredictTheWinner(vector<int>& nums) {
        int n = nums.size();
        vector<vector<int>> dp(n,vector<int>(n));
        for (int i = 0; i < n; i++) {
            dp[i][i] = nums[i];
        }
        for (int i = 1; i < n; i++) {
            for (int j = 0; j + i < n; j++) {
                dp[j][j+i] = max(nums[j+i]-dp[j][j+i-1], nums[j] - dp[j+1][j+i]);
            }
        }
        return dp[0][n-1] >= 0;
    }
};
```

Reference: [https://discuss.leetcode.com/topic/76327/c-dp-solution-with-explanation](https://discuss.leetcode.com/topic/76327/c-dp-solution-with-explanation)