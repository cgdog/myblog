---
title: leetcode 462. Minimum Moves to Equal Array Elements II
id: 832
categories:
  - algorithm
date: 2017-02-12 17:31:39
tags:
  - leetcode
  - math
---

[462\. Minimum Moves to Equal Array Elements II](https://leetcode.com/problems/minimum-moves-to-equal-array-elements-ii/)

Given a **non-empty** integer array, find the minimum number of moves required to make all array elements equal, where a move is incrementing a selected element by 1 or decrementing a selected element by 1.

You may assume the array's length is at most 10,000.

**Example:**
```
    Input:
    [1,2,3]

    Output:
    2

    Explanation:
    Only two moves are needed (remember each move increments or decrements one element):

    [1,2,3]  =>  [2,2,3]  =>  [2,2,2]
```


``` cpp
class Solution {
public:
    int minMoves2(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int m = nums[nums.size() / 2];
        int count = 0;
        for (int i = 0; i < nums.size(); i++) {
            count += (int)abs(m - nums[i]);
        }
        return count;
    }
};
```