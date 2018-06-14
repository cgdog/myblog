---
title: leetcode 406. Queue Reconstruction by Height
id: 840
categories:
  - C++
date: 2017-03-19 16:21:49
tags:
  - leetcode
---

[406\. Queue Reconstruction by Height](https://leetcode.com/problems/queue-reconstruction-by-height/#/description)

Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers (h, k), where h is the height of the person and k is the number of people in front of this person who have a height greater than or equal to h. Write an algorithm to reconstruct the queue.

**Note:**

The number of people is less than 1,100.

**Example**


```
    Input:  
    `[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]`

    Output:  
    `[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]`
```

    Solution:


``` cpp
    class Solution {
    public:
        vector<pair<int, int>> reconstructQueue(vector<pair<int, int>>& people) {
            vector<pair<int, int>> res;
            sort(people.begin(), people.end(), [](pair<int, int> a, pair<int, int> b) {
                return a.first > b.first || (a.first == b.first && a.second < b.second);
            });
            for (int i = 0; i < people.size(); i++) {
                res.insert(res.begin()+people[i].second, people[i]);
            }
            return res;
        }
    };
```
**Reference:**

[https://discuss.leetcode.com/topic/60394/easy-concept-with-python-c-java-solution/4](https://discuss.leetcode.com/topic/60394/easy-concept-with-python-c-java-solution/4)