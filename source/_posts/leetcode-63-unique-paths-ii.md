---
title: leetCode 63. Unique Paths II
id: 782
categories:
  - algorithm
date: 2017-01-06 11:02:08
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[63\. Unique Paths II](https://leetcode.com/problems/unique-paths-ii/)

Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,   
There is one obstacle in the middle of a 3x3 grid as illustrated below.  

    [
      [0,0,0],
      [0,1,0],
      [0,0,0]
    ]

The total number of unique paths is 2.

**Note:** m and n will be at most 100.

My naive DP solution with O(n) space:
(There are too many useless `if` condition checkings.)



``` cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<int> path(m, 0);
        path[0] = obstacleGrid[0][0] == 0 ? 1 : 0;
        for (int i = 1; i < m; i++) {
            if (obstacleGrid[i][0] != 1 && path[i-1] != 0) {
                path[i] = 1;
            }
        }
        for (int i = 1; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (obstacleGrid[j][i] == 1) {
                    path[j] = 0;
                } else if(j > 0) {
                    if ((obstacleGrid[j][i-1] == 1 || path[j] == -1) && (obstacleGrid[j-1][i] != 1 && path[j-1] != -1)) {
                        path[j] = path[j-1];
                    } else if ((obstacleGrid[j][i-1] == 1 || path[j] == -1) && (obstacleGrid[j-1][i] == 1 || path[j-1] == -1)) {
                        path[j] = 0;
                    } else if ((obstacleGrid[j][i-1] != 1 || path[j] != -1) && (obstacleGrid[j-1][i] != 1 && path[j-1] != -1)) {
                        path[j] += path[j-1];
                    }
                }
            }
        }
        return path[m-1];
    }
};
```

Solution 2 (neat code):



``` cpp
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<int> path(m, 0);
        path[0] = !obstacleGrid[0][0];
        for (int i = 1; i < m; i++) {
            if (!obstacleGrid[i][0] && path[i-1])
                path[i] = 1;
        }

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if (obstacleGrid[j][i] == 1) {
                    path[j] = 0;
                } else if(j > 0) {
                    path[j] += path[j-1];
                }
            }
        }
        return path[m-1];
    }
};
```