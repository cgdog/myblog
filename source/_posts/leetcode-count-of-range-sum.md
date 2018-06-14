---
title: leetCode Count of Range Sum
id: 652
categories:
  - algorithm
date: 2016-11-01 15:56:20
tags:
  - Divide and Conquer
  - leetcode
---

[Count of Range Sum](https://leetcode.com/problems/count-of-range-sum/)


``` cpp
class Solution {
public:
    int countRangeSumMerge(vector<long> &sums, int start, int end, int lower, int upper) {
        if (end < start) return 0;
        if (start == end) return (sums[start] >= lower && sums[end] <= upper) ? 1 : 0;

        int mid = start + (end - start) / 2;
        int count = countRangeSumMerge(sums, start, mid, lower, upper) + countRangeSumMerge(sums, mid + 1, end, lower, upper);
        int m = mid + 1, n = mid + 1;
        vector<long> cache(end - start + 1, 0);
        for (int i = start; i <= mid; i++) {
            while (m <= end && sums[m] - sums[i] < lower) m++;
            while (n <= end && sums[n] - sums[i] <= upper) n++;
            count += n - m;
        }
        for (int i = start, j = mid + 1, k = start; k <= end; k++) {
            cache[k - start] = (i <= mid) && (j > end || sums[i] < sums[j]) ? sums[i++] : sums[j++];
        }
        for (int k = start; k <= end; k++) {
            sums[k] = cache[k - start];
        }
        return count;
    }
    int countRangeSum(vector<int>& nums, int lower, int upper) {
        int n = nums.size();
        if (n == 0) return 0;
        vector<long> sums(n + 1, 0);
        for (int i = 0; i < n; i++) {
            sums[i + 1] = sums[i] + nums[i];
        }
        return countRangeSumMerge(sums, 1, n, lower, upper);
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/33993/8-line-multiset-c-solution-100ms-also-binary-search-tree-180ms-mergesort-52ms](https://discuss.leetcode.com/topic/33993/8-line-multiset-c-solution-100ms-also-binary-search-tree-180ms-mergesort-52ms)