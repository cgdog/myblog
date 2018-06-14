---
title: leetcode 403. Frog Jump
id: 786
categories:
  - algorithm
date: 2017-01-08 10:35:30
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[403\. Frog Jump](https://leetcode.com/problems/frog-jump/)

A frog is crossing a river. The river is divided into x units and at each unit there may or may not exist a stone. The frog can jump on a stone, but it must not jump into the water.

Given a list of stones' positions (in units) in sorted ascending order, determine if the frog is able to cross the river by landing on the last stone. Initially, the frog is on the first stone and assume the first jump must be 1 unit.

If the frog's last jump was k units, then its next jump must be either k - 1, k, or k + 1 units. Note that the frog can only jump in the forward direction.

**Note:**

The number of stones is ≥ 2 and is &lt; 1,100.

Each stone's position will be a non-negative integer &lt; 231.

The first stone's position is always 0.

Example 1:

    `[0,1,3,5,6,8,12,17]`
    

    There are a total of 8 stones.

    The first stone at the 0th unit, second stone at the 1st unit,

    third stone at the 3rd unit, and so on...

    The last stone at the 17th unit.

    Return true. The frog can jump to the last stone by jumping

    1 unit to the 2nd stone, then 2 units to the 3rd stone, then

    2 units to the 4th stone, then 3 units to the 6th stone,

    4 units to the 7th stone, and 5 units to the 8th stone.

    Example 2:

    `[0,1,2,3,4,8,9,11]`

Return false. There is no way to jump to the last stone as

the gap between the 5th and 6th stone is too large.

The solution is Memory Limit Exceeded, although its results are right:



``` cpp
class Solution {
public:
    bool canCross(vector<int>& stones) {
        if (stones.size() == 0) return true;
        unordered_map<int, unordered_set<int>> mp(stones.size());
        mp[0].insert(1);
        for (int i = 0; i < stones.size()-1; i++) {
            for (int step : mp[stones[i]]) {
                int next_stone = step + stones[i];
                if (next_stone == stones.back())
                    return true;
                else {
                    mp[next_stone].insert(step);
                    mp[next_stone].insert(step+1);
                    if (step > 1)
                        mp[next_stone].insert(step-1);
                }
            }
        }
        return false;
    }
};
```

[https://discuss.leetcode.com/topic/59903/very-easy-to-understand-java-solution-with-explanations](https://discuss.leetcode.com/topic/59903/very-easy-to-understand-java-solution-with-explanations)

DP solution:



``` cpp
class Solution {
public:
    bool canCross(vector<int>& stones) {
        unordered_map<int, unordered_set<int>> dp;
        dp[0].insert(0);
        for (int stone : stones) {
            for (int step : dp[stone]) {
                if (step - 1 > 0) dp[stone+step-1].insert(step-1);
                dp[stone+step].insert(step);
                dp[stone+step+1].insert(step+1);
            }
        }
        return !dp[stones.back()].empty();
    }
};
```

[https://discuss.leetcode.com/topic/60194/c-9-lines-o-n-2-iterative-dp-solution/18](https://discuss.leetcode.com/topic/60194/c-9-lines-o-n-2-iterative-dp-solution/18)