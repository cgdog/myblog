---
title: leetCode Combination Sum IV
id: 731
categories:
  - algorithm
date: 2016-12-07 20:41:41
tags:
  - Dynamic programming
  - leetcode
---

[Combination Sum IV](https://leetcode.com/problems/combination-sum-iv/)

Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

Example:

    nums = [1, 2, 3]
    target = 4

    The possible combination ways are:
    (1, 1, 1, 1)
    (1, 1, 2)
    (1, 2, 1)
    (1, 3)
    (2, 1, 1)
    (2, 2)
    (3, 1)

    Note that different sequences are counted as different combinations.

    Therefore the output is 7.
    

    Follow up:
    What if negative numbers are allowed in the given array?
    How does it change the problem?
    What limitation we need to add to the question to allow negative numbers?

    Solution 1:



``` cpp
class Solution {
    public:

        int helper(vector<int>& dp, vector<int>& nums, int target) {
            if (dp[target] != -1) {
                return dp[target];
            }
            int res = 0;
            for (int i = 0; i < nums.size(); i++) {
                if (target >= nums[i]) {
                    res += helper(dp, nums, target-nums[i]);
                }
            }
            dp[target] = res;
            return res;
        }
        int combinationSum4(vector<int>& nums, int target) {
            vector<int> dp(target+1, -1);
            dp[0] = 1;
            helper(dp, nums, target);
            return dp[target];
        }
    };
```

    Solution 2:



``` cpp
class Solution {
    public:

        int helper(vector<int>& dp, vector<int>& nums, int target) {
            if (dp[target] != -1) {
                return dp[target];
            }
            int res = 0;
            for (int i = 0; i < nums.size(); i++) {
                if (target >= nums[i]) {
                    res += helper(dp, nums, target-nums[i]);
                }
            }
            dp[target] = res;
            return res;
        }
        int combinationSum4(vector<int>& nums, int target) {
            vector<int> dp(target+1, -1);
            dp[0] = 1;
            helper(dp, nums, target);
            return dp[target];
        }
    };
```
Reference:[https://discuss.leetcode.com/topic/52302/1ms-java-dp-solution-with-detailed-explanation](https://discuss.leetcode.com/topic/52302/1ms-java-dp-solution-with-detailed-explanation)