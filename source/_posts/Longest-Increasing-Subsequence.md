---
title: 'Longest Increasing Subsequence'
tags:
  - Dynamic Programming
  - LIS
  - leetcode
id: 390
categories:
  - algorithm
date: 2016-09-16 17:55:52
---

[Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

Given an unsorted array of integers, find the length of longest increasing subsequence.

For example,

Given [10, 9, 2, 5, 3, 7, 101, 18],

The longest increasing subsequence is [2, 3, 7, 101], therefore the length is 4\. Note that there may be more than one LIS combination, it is only necessary for you to return the length.

Your algorithm should run in O(n2) complexity.

Follow up: Could you improve it to O(n log n) time complexity?



``` cpp
// O(n^2) 106ms
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        if (n <= 1) {
            return n;
        }
        vector<int> dp(n,1);
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[j] < nums[i] && dp[j] + 1 > dp[i]) {
                    dp[i] = dp[j] + 1;
                }
            }
        }

        return *(max_element(dp.begin(), dp.end()));
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/30721/my-easy-to-understand-o-n-2-solution-using-dp-with-video-explanation](https://discuss.leetcode.com/topic/30721/my-easy-to-understand-o-n-2-solution-using-dp-with-video-explanation)

### Follow up: O(nlgn)



``` cpp
// O(nlgn) 3ms
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> res;
        for (int i = 0; i < nums.size(); i++) {
            vector<int>::iterator iter = lower_bound(res.begin(), res.end(), nums[i]);
            if (iter == res.end()) {
                res.push_back(nums[i]);
            } else {
                *iter = nums[i];
            }
        }

        return res.size();
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/28696/9-lines-c-code-with-o-nlogn-complexity](https://discuss.leetcode.com/topic/28696/9-lines-c-code-with-o-nlogn-complexity)
> 
> Good Links:[http://stackoverflow.com/questions/2631726/how-to-determine-the-longest-increasing-subsequence-using-dynamic-programming](http://stackoverflow.com/questions/2631726/how-to-determine-the-longest-increasing-subsequence-using-dynamic-programming)
>   [http://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/](http://www.geeksforgeeks.org/longest-monotonically-increasing-subsequence-size-n-log-n/)