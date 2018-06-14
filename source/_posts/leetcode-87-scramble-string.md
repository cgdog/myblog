---
title: leetcode 87. Scramble String
id: 803
categories:
  - algorithm
date: 2017-01-18 17:16:20
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[87&#46; Scramble String](https://leetcode.com/problems/scramble-string/)

Given a string s1, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.

Below is one possible representation of s1 = "great":

        great
       /    \
      gr    eat
     / \    /  \
    g   r  e   at
               / \
              a   t
    `</pre>

    To scramble the string, we may choose any non-leaf node and swap its two children.

    For example, if we choose the node "gr" and swap its two children, it produces a scrambled string `"rgeat"`.

    <pre>`    rgeat
       /    \
      rg    eat
     / \    /  \
    r   g  e   at
               / \
              a   t
    `</pre>

    We say that `"rgeat"` is a scrambled string of `"great"`.

    Similarly, if we continue to swap the children of nodes "eat" and "at", it produces a scrambled string "rgtae".

    <pre>`    rgtae
       /    \
      rg    tae
     / \    /  \
    r   g  ta  e
           / \
          t   a

We say that `"rgtae"` is a scrambled string of `"great"`.

Given two strings s1 and s2 of the same length, determine if s2 is a scrambled string of s1.

Recursive solution:



``` cpp
class Solution {
public:
    bool isScramble(string s1, string s2) {
        if (s1 == s2) return true;
        int len = s1.length();
        int count[256] = {0};
        for (int i = 0; i < len; i++) {
            count[s1[i]]++;
            count[s2[i]]--;
        }
        for (int i = 0; i < 256; i++) {
            if (count[i] != 0) {
                return false;
            }
        }
        for (int i = 1; i < len; i++) {
            if (isScramble(s1.substr(0, i), s2.substr(0, i)) && isScramble(s1.substr(i), s2.substr(i))) {
                return true;
            }
            if (isScramble(s1.substr(0, i), s2.substr(len-i)) && isScramble(s1.substr(i), s2.substr(0, len-i))) {
                return true;
            }
        }
        return false;
    }
};
```

Reference:[https://discuss.leetcode.com/topic/14337/share-my-4ms-c-recursive-solution](https://discuss.leetcode.com/topic/14337/share-my-4ms-c-recursive-solution)

DP solution:[https://discuss.leetcode.com/topic/20094/my-c-solutions-recursion-with-cache-dp-recursion-with-cache-and-pruning-with-explanation-4ms](https://discuss.leetcode.com/topic/20094/my-c-solutions-recursion-with-cache-dp-recursion-with-cache-and-pruning-with-explanation-4ms)