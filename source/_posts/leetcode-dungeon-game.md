---
title: leetCode Dungeon Game
tags:
  - Dynamic Programming
  - leetcode
id: 381
categories:
  - algorithm
date: 2016-09-16 12:03:30
---

[Dungeon Game](https://leetcode.com/problems/dungeon-game/)



``` cpp
class Solution {
public:
    int calculateMinimumHP(vector<vector<int>>& dungeon) {
        vector<vector<int> > dp(dungeon.size() + 1, vector<int>(dungeon[0].size()+1, INT_MAX));

        dp[dungeon.size()][dungeon[0].size()-1] = 1;
        dp[dungeon.size() - 1][dungeon[0].size()] = 1;
        for (int row = dungeon.size() - 1; row >= 0; row--) {
            for (int col = dungeon[0].size() - 1; col >= 0; col--) {
                dp[row][col] = min(dp[row+1][col], dp[row][col+1]) - dungeon[row][col];
                dp[row][col] = dp[row][col] <= 0 ? 1 : dp[row][col];
            }
        }
        return dp[0][0];
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/6912/c-dp-solution/12](https://discuss.leetcode.com/topic/6912/c-dp-solution/12)

### [Explanation](https://discuss.leetcode.com/topic/9271/my-java-solution-with-explanation-in-detail)

With a health array to store each grid's health, we should get the result at &#91;0&#93;&#91;0&#93;.

Now the question become to how to create a health array using dungeon.

dungeon

-2,-3,3

-5,-10,1

10,30,-5

From the Dungeon grid, we can simply compute health for the [last row][last column].

Now we get

?,?,?

?,?,?

?,?,6

Now because the knight can only move rightward or downward in each step, we can compute all the health value for last row from right to left using its rightward neighbor. we can also compute all the health value for last column from bottom to up using its downward neighbor.

?,?,2

?,?,5

1,1,6

Now, we can compute all the health value using its downward neighbor and rightward neighbor(we use the min value of these 2 health value).

7,5,2

6,11,5

1,1,6

Now we get the answer &#91;0&#93;&#91;0&#93;, which is 7.