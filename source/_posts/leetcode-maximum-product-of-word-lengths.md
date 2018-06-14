---
title: leetCode Maximum Product of Word Lengths
tags:
  - Bit manipulation
  - leetcode
id: 421
categories:
  - algorithm
date: 2016-09-23 22:02:18
---

[Maximum Product of Word Lengths](https://leetcode.com/problems/maximum-product-of-word-lengths/)

Given a string array words, find the maximum value of length(word[i]) * length(word[j]) where the two words do not share common letters. You may assume that each word will contain only lower case letters. If no such two words exist, return 0.

Example 1:

Given ["abcw", "baz", "foo", "bar", "xtfn", "abcdef"]

Return 16

The two words can be "abcw", "xtfn".

Example 2:

Given ["a", "ab", "abc", "d", "cd", "bcd", "abcd"]

Return 4

The two words can be "ab", "cd".

Example 3:

Given ["a", "aa", "aaa", "aaaa"]

Return 0

No such pair of words.


``` cpp
class Solution {
public:
    int maxProduct(vector<string>& words) {
        vector<int> mask(words.size(), 0);
        int res = 0;
        for (int i = 0; i < words.size(); i++) {
            for (int j = 0; j < words[i].size(); j++) {
                mask[i] |= 1 << (words[i][j]-'a');
            }
        }

        for (int i = 0; i < mask.size(); i++) {
            for (int j = i+1; j < mask.size();j++) {
                if (!(mask[i] & mask[j])) {
                    res = max(res, int(words[i].size()*words[j].size()));
                }
            }
        }
        return res;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/31766/bit-shorter-c](https://discuss.leetcode.com/topic/31766/bit-shorter-c)