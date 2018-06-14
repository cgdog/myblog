---
title: leetcode 120. Triangle
id: 776
categories:
  - algorithm
date: 2017-01-04 23:57:55
tags:
  - Dynamic programming
  - leetcode
---

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

    For example, given the following triangle
    [
         [2],
        [3,4],
       [6,5,7],
      [4,1,8,3]
    ]

The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:

Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

Method 1\. O(n) space.



``` cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        if (triangle.size() < 1) return 0;
        vector<int> minlens(triangle.back());
        for (int i = triangle.size() - 2; i >= 0; i--) {
            for (int j = 0; j <= i; j++) {
                minlens[j] = min(minlens[j], minlens[j+1]) + triangle[i][j];
            }
        }
        return minlens[0];
    }
};
```

Method 2\. O(1) space, but modify the input vector.



``` cpp
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        if (triangle.size() < 1) return 0;
        for (int i = triangle.size()-2; i >= 0; i--) {
            for (int j = 0; j < triangle[i].size(); j++) {
                triangle[i][j] += min(triangle[i+1][j], triangle[i+1][j+1]);
            }
        }
        return triangle[0][0];
    }
};
```

[https://discuss.leetcode.com/topic/1669/dp-solution-for-triangle](https://discuss.leetcode.com/topic/1669/dp-solution-for-triangle)