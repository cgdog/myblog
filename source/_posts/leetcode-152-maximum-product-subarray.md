---
title: leetcode 152. Maximum Product Subarray
id: 816
categories:
  - algorithm
date: 2017-01-19 15:31:23
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[152\. Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array `[2,3,-2,4]`,

the contiguous subarray `[2,3]` has the largest product = `6`.

Brute force solution (Time Limit Exceeded):



``` cpp
    class Solution {
    public:
        int maxProduct(vector&lt;int&gt;&amp; nums) {
            int n = nums.size();
            if (n == 0) return 0;
            int res = nums[0];
            for (int i = 0; i &lt; n; i++) {
                res = max(res, nums[i]);
                for (int j = i+1; j &lt; n; j++) {
                    int tmp = 1;
                    for (int k = i; k &lt;= j; k++)
                        tmp *= nums[k];
                    res = max(res, tmp);
                }
            }
            return res;
        }
    };
```

    DP solution (O(1) space):



``` cpp
    class Solution {

    <pre>`public:
        int maxProduct(vector&lt;int&gt;&amp; nums) {
            int n = nums.size();
            if (n == 0) return 0;
            int maxProdPre = nums[0];
            int minProdPre = maxProdPre;
            int curProd = maxProdPre;
            int maxProd, minProd;
            for (int i = 1; i &lt; n; i++) {
                maxProd = max(nums[i], max(maxProdPre*nums[i], minProdPre * nums[i]));
                minProd = min(nums[i], min(minProdPre*nums[i], maxProdPre*nums[i]));
                curProd = max(curProd, maxProd);
                maxProdPre = maxProd;
                minProdPre = minProd;
            }
            return curProd;
        }
    };
```

Reference:

1\. [https://discuss.leetcode.com/topic/3607/sharing-my-solution-o-1-space-o-n-running-time](https://discuss.leetcode.com/topic/3607/sharing-my-solution-o-1-space-o-n-running-time)
2\. [https://discuss.leetcode.com/topic/3581/share-my-dp-code-that-got-ac](https://discuss.leetcode.com/topic/3581/share-my-dp-code-that-got-ac)