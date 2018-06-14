---
title: leetCode 494. Target Sum
id: 819
categories:
  - algorithm
date: 2017-02-08 17:40:27
tags:
  - C++
  - DFS
  - Dynamic programming
  - leetcode
---

[494\. Target Sum](https://leetcode.com/problems/target-sum/?tab=Description)

You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

**Example 1:**

    Input: nums is [1, 1, 1, 1, 1], S is 3\. 
    Output: 5
    Explanation: 

    -1+1+1+1+1 = 3
    +1-1+1+1+1 = 3
    +1+1-1+1+1 = 3
    +1+1+1-1+1 = 3
    +1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.

**Note:**

The length of the given array is positive and will not exceed 20.

The sum of elements in the given array will not exceed 1000.

Your output answer is guaranteed to be fitted in a 32-bit integer.

DFS solution 1 (480ms):



``` cpp
class Solution {
public:
    int result;
    int findTargetSumWays(vector<int>& nums, int S) {
        result = 0;
        DFS(0, 0, nums, S);
        return result;
    }
    void DFS(int sum, int cnt, vector<int>& nums, int S) {
        if (cnt == nums.size()) {
            if (sum == S) {
                result++;
            }
            return;
        }
        DFS(sum + nums[cnt], cnt+1, nums, S);
        DFS(sum - nums[cnt], cnt+1, nums, S);
    }
};
```

Reference: [http://blog.csdn.net/liuchuo/article/details/54670609](http://blog.csdn.net/liuchuo/article/details/54670609)

DFS Solution 2 (515ms):



``` cpp
class Solution {
public:
    unordered_map<string, int> cache;
    int findTargetSumWays(vector<int>& nums, int S) {
        return DFS(0, 0, nums, S);
    }
    int DFS(int sum, int cnt, vector<int>& nums, int S) {

        string key = to_string(sum) +"-"+to_string(cnt);
        if (cache.find(key) != cache.end()) {
            return cache[key];
        }
        if (cnt == nums.size()) {
            if (sum == S) {
                return 1;
            }
            return 0;
        }
        int add = DFS(sum + nums[cnt], cnt+1, nums, S);
        int minus = DFS(sum - nums[cnt], cnt+1, nums, S);
        cache[key] = add + minus;
        return cache[key];
    }
};
```

Reference: [https://discuss.leetcode.com/topic/76245/java-simple-dfs-with-memorization](https://discuss.leetcode.com/topic/76245/java-simple-dfs-with-memorization)

O(ns) iterative DP solution using subset sum with explanation. 9ms:



``` cpp
class Solution {
public:
    int findTargetSumWays(vector<int>& nums, int S) {
        int sum = accumulate(nums.begin(), nums.end(), 0);
        return sum < S || (sum + S) & 1 ? 0 : subset(nums, (sum + S) >> 1);
    }
    int subset(vector<int>& nums, int s) {
        vector<int> dp(s+1, 0);
        dp[0] = 1;
        for (int i = 0; i < nums.size(); i++) {
            for (int j = s; j >= nums[i]; j--) {
                dp[j] += dp[j-nums[i]];
            }
        }
        return dp[s];
    }
};
```

Reference: [https://discuss.leetcode.com/topic/76243/java-15-ms-c-3-ms-o-ns-iterative-dp-solution-using-subset-sum-with-explanation](https://discuss.leetcode.com/topic/76243/java-15-ms-c-3-ms-o-ns-iterative-dp-solution-using-subset-sum-with-explanation)