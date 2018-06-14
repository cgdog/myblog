---
title: leetcode 453. Minimum Moves to Equal Array Elements
id: 830
categories:
  - algorithm
date: 2017-02-12 17:13:23
tags:
  - C++
  - leetcode
---

[453\. Minimum Moves to Equal Array Elements](https://leetcode.com/problems/minimum-moves-to-equal-array-elements/)

Given a **non-empty** integer array of size n, find the minimum number of moves required to make all array elements equal, where a move is incrementing n - 1 elements by 1.

**Example:**
```
    Input:
    [1,2,3]

    Output:
    3

    Explanation:
    Only three moves are needed (remember each move increments two elements):

    [1,2,3]  =>  [2,3,3]  =>  [3,4,3]  =>  [4,4,4]
```



``` cpp
class Solution {
public:
    int minMoves(vector<int>& nums) {
        int min_num = nums[0];
        int sum = 0;
        for (int num : nums) {
            min_num = min(min_num, num);
            sum += num;
        }

        return sum - min_num * nums.size();
    }
};
```

Reference: [https://discuss.leetcode.com/topic/66557/java-o-n-solution-short/2](https://discuss.leetcode.com/topic/66557/java-o-n-solution-short/2)