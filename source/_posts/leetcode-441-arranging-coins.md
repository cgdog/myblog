---
title: leetcode 441. Arranging Coins
id: 834
categories:
  - algorithm
date: 2017-02-12 20:42:23
tags:
  - C++
  - leetcode
  - math
---

[441\. Arranging Coins](https://leetcode.com/problems/arranging-coins/)

You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

**Example 1:**

    n = 5

    The coins can form the following rows:
    ¤
    ¤ ¤
    ¤ ¤

    Because the 3rd row is incomplete, we return 2.
    `</pre>

    **Example 2:**

    <pre>`n = 8

    The coins can form the following rows:
    ¤
    ¤ ¤
    ¤ ¤ ¤
    ¤ ¤

    Because the 4th row is incomplete, we return 3.
    `</pre>

    My solution:



``` cpp
class Solution {
    public:
        int arrangeCoins(int n) {
            if (n == 0) return 0;
            long long sum = 1;
            int i = 1;
            while (sum < n) {
                sum += ++i;
            }
            if (sum > n) i--;
            return i;
        }
    };

```
Other methods:

Using Binary Search and Mathematics: [https://discuss.leetcode.com/topic/65593/java-clean-code-with-explanations-and-running-time-2-solutions](https://discuss.leetcode.com/topic/65593/java-clean-code-with-explanations-and-running-time-2-solutions)

Reference: [https://zh.wikipedia.org/wiki/%E4%B8%89%E8%A7%92%E5%BD%A2%E6%95%B8](https://zh.wikipedia.org/wiki/%E4%B8%89%E8%A7%92%E5%BD%A2%E6%95%B8)