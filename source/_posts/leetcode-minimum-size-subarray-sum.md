---
title: leetCode Minimum Size Subarray Sum
id: 384
categories:
  - algorithm
date: 2016-09-16 15:53:38
tags:
  - leetcode
---

[Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/)

Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return 0 instead.

For example, given the array [2,3,1,2,4,3] and s = 7,
the subarray [4,3] has the minimal length under the problem constraint.

### method one:



``` cpp
// 3ms O(n) two pointer method:
class Solution {
public:
    int minSubArrayLen(int s, vector<int>& nums) {
        int n = nums.size(), left = 0, sum = 0, min_len = INT_MAX;
        for (int i = 0; i < n; i++) {
            sum += nums[i];
            while (sum >= s) {
                min_len = min(min_len, i - left + 1);
                sum -= nums[left++];
            }
        }
        return min_len == INT_MAX ? 0 : min_len;
    }
};
```

### method two:



``` cpp
// 6ms O(nlgn)
class Solution {
public:

    int upper_bound(vector<int>& sums, int left, int right, int target) {
        while (left < right) {
            int mid = left + ((right - left) >> 1);
            if (sums[mid] <= target) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return sums[right] > target ? right : -1;
    }

    int minSubArrayLen(int s, vector<int>& nums) {
        int n = nums.size(), minlen = INT_MAX;
        vector<int> sums(n+1, 0);
        for (int i = 1; i <= n; i++) {
            sums[i] = sums[i-1] + nums[i-1];
        }

        for (int i = 1; i <= n; i++) {
            if (sums[i] >= s) {
                int p = upper_bound(sums, 0, i, sums[i] - s);
                if (p != -1) {
                    minlen = min(i-p+1, minlen);
                }
            }
        }
        return minlen <= n ? minlen : 0;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/17063/4ms-o-n-8ms-o-nlogn-c/2](https://discuss.leetcode.com/topic/17063/4ms-o-n-8ms-o-nlogn-c/2)