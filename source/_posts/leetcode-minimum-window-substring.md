---
title: leetCode Minimum Window Substring
id: 403
categories:
  - algorithm
date: 2016-09-20 00:19:17
tags:
  - leetcode
---

[Minimum Window Substring](https://leetcode.com/submissions/detail/74938487/)

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

For example,
`S = "ADOBECODEBANC"`  
`T = "ABC"`  
Minimum window is "BANC".

Note:
If there is no such window in S that covers all characters in T, return the empty string "".

If there are multiple such windows, you are guaranteed that there will always be only one unique minimum window in S.




``` cpp
class Solution {
public:
    string minWindow(string s, string t) {
        int n = s.size(), len = t.size();
        vector<int> m(128, 0);
        for (int i = 0; i < len; i++) {
            m[t[i]]++;
        }
        int counter = t.size(), begin = 0, end = 0, head = 0, d = INT_MAX;
        while (end < n) {
            if (m[s[end++]]-- > 0) counter--;
            while (counter == 0) {
                if (end - begin < d) {
                    d = end - (head=begin);
                }
                if (m[s[begin++]]++ == 0) counter++;
            }
        }
        return d == INT_MAX ? "" : s.substr(head, d);
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/30941/here-is-a-10-line-template-that-can-solve-most-substring-problems](https://discuss.leetcode.com/topic/30941/here-is-a-10-line-template-that-can-solve-most-substring-problems) good link!!!