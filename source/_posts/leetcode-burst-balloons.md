---
title: leetCode Burst Balloons
id: 733
categories:
  - algorithm
date: 2016-12-07 22:19:28
tags:
  - Divide and Conquer
  - Dynamic programming
  - leetcode
---

# [Burst Balloons](https://leetcode.com/problems/burst-balloons/)

Given n balloons, indexed from 0 to n-1\. Each balloon is painted with a number on it represented by array nums. You are asked to burst all the balloons. If the you burst balloon i you will get nums[left] * nums[i] * nums[right] coins. Here left and right are adjacent indices of i. After the burst, the left and right then becomes adjacent.

Find the maximum coins you can collect by bursting the balloons wisely.

Note: 
(1) You may imagine nums[-1] = nums[n] = 1\. They are not real therefore you can not burst them.

(2) 0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100

Example:

Given [3, 1, 5, 8]

Return 167

       nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
       coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167
    

    Solution 1:



``` cpp
class Solution {
    public:
        int burst(vector<vector<int>>& memo, vector<int>& nums, int left, int right) {
            if (left + 1 == right) return 0;
            if (memo[left][right] > 0) return memo[left][right];
            int ans = 0;
            for (int i = left+1; i < right; i++) {
                ans = max(ans, nums[left]*nums[i]*nums[right]+burst(memo, nums, left, i)+burst(memo, nums, i, right));
            }
            memo[left][right] = ans;
            return ans;
        }
        int maxCoins(vector<int>& inums) {
            vector<int> nums(inums.size()+2);
            int n = 1;
            for (int i = 0; i < inums.size(); i++) {
                if (inums[i]>0) nums[n++] = inums[i];
            }
            nums[0] = nums[n++] = 1;
            vector<vector<int>> memo(n,vector<int>(n));
            return burst(memo, nums, 0, n-1);
        }
    };
```

    Solution 2:



``` cpp
class Solution {
    public:

        int maxCoins(vector<int>& inums) {
            vector<int> nums(inums.size()+2);
            int n = 1;
            for (int i = 0; i < inums.size(); i++) {
                if (inums[i]>0) nums[n++] = inums[i];
            }
            nums[0] = nums[n++] = 1;
            vector<vector<int>> dp(n,vector<int>(n));
            for (int k = 2; k < n; k++) {
                for (int left = 0; left < n-k; left++) {
                    int right = left+k;
                    for (int i = left+1; i < right; i++) {
                        dp[left][right] = max(dp[left][right], nums[left]*nums[i]*nums[right]+dp[left][i]+dp[i][right]);
                    }
                }
            }
            return dp[0][n-1];
        }
    };
```

Reference:[https://discuss.leetcode.com/topic/30746/share-some-analysis-and-explanations](https://discuss.leetcode.com/topic/30746/share-some-analysis-and-explanations)