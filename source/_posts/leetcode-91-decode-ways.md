---
title: leetcode 91. Decode Ways
id: 814
categories:
  - algorithm
date: 2017-01-19 12:29:33
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[91\. Decode Ways](https://leetcode.com/problems/decode-ways/)

A message containing letters from `A-Z` is being encoded to numbers using the following mapping:
```
    'A' -> 1
    'B' -> 2
    ...
    'Z' -> 26
```

    Given an encoded message containing digits, determine the total number of ways to decode it.

    **For example,**

    Given encoded message `"12"`, it could be decoded as `"AB"` (1 2) or `"L"` (12).

    The number of ways decoding `"12"` is 2.


``` cpp
class Solution {
    public:
        int numDecodings(string s) {
            int n = s.length();
            if (n == 0) return 0;
            int second = 1;
            int first = s[n-1] == '0' ? 0 : 1;
            int res = first;
            for (int i = n-2; i >= 0; i--) {
                if (s[i] != '0') {
                    if (s[i] < '2' || s[i] == '2' && s[i+1] <= '6') {
                        res = second + first;
                    } else {
                        res = first;
                    }
                } else {
                    res = 0;
                }
                second = first;
                first = res;
            }
            return res;
        }
    };
```

Reference:[https://discuss.leetcode.com/topic/2562/dp-solution-java-for-reference](https://discuss.leetcode.com/topic/2562/dp-solution-java-for-reference)