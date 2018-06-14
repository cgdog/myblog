---
title: leetCode Subsets
tags:
  - Bit manipulation
  - leetcode
id: 427
categories:
  - algorithm
date: 2016-09-24 15:13:08
---

[Subsets](https://leetcode.com/problems/subsets/)

Given a set of distinct integers, nums, return all possible subsets.

Note: The solution set must not contain duplicate subsets.

For example, If nums = [1,2,3], a solution is:

<pre>[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
</pre>

Iterative 6ms



``` cpp
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        int n = nums.size();

        vector<vector<int>> res(1, vector<int>());
        for (int i = 0; i < n; i++) {
            int m = res.size();
            for (int j = 0; j < m; j++) {
                res.push_back(res[j]);
                res.back().push_back(nums[i]);
            }
        }
        return res;
    }
};
```

Bit manipulation 9ms

```
class Solution {
public:
    vector<vector<int>> subsets(vector<int>& nums) {
        int elem_size = nums.size();
        int sub_size = (int)pow(2, elem_size);
        vector<vector<int>> res(sub_size, vector<int>());
        for (int i = 0; i < elem_size; i++) {
            for (int j = 0; j < sub_size; j++) {
                if  (j >> i & 1) {
                    res[j].push_back(nums[i]);
                }
            }
        }
        return res;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/19110/c-recursive-iterative-bit-manipulation-solutions-with-explanations](https://discuss.leetcode.com/topic/19110/c-recursive-iterative-bit-manipulation-solutions-with-explanations)
> 
> A link may be useful:[https://discuss.leetcode.com/topic/46159/a-general-approach-to-backtracking-questions-in-java-subsets-permutations-combination-sum-palindrome-partitioning](https://discuss.leetcode.com/topic/46159/a-general-approach-to-backtracking-questions-in-java-subsets-permutations-combination-sum-palindrome-partitioning)