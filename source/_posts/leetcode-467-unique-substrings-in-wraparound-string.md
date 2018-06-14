---
title: leetcode 467. Unique Substrings in Wraparound String
id: 797
categories:
  - algorithm
date: 2017-01-17 18:22:36
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[467\. Unique Substrings in Wraparound String](https://leetcode.com/problems/unique-substrings-in-wraparound-string/)

Consider the string s to be the infinite wraparound string of "abcdefghijklmnopqrstuvwxyz", so s will look like this: "...zabcdefghijklmnopqrstuvwxyzabcdefghijklmnopqrstuvwxyzabcd....".

Now we have another string p. Your job is to find out how many unique non-empty substrings of p are present in s. In particular, your input is the string p and you need to output the number of different non-empty substrings of p in the string s.

Note: p consists of only lowercase English letters and the size of p might be over 10000.

**Example 1:**

    Input: "a"
    Output: 1
    Explanation: Only the substring "a" of string "a" is in the string s.
    

    **Example 2:**

    `Input: "cac"
    Output: 2
    Explanation: There are two substrings "a", "c" of string "cac" in the string s.
    `

    **Example 3:**

    `Input: "zab"
    Output: 6
    Explanation: There are six substrings "z", "a", "b", "za", "ab", "zab" of string "zab" in the string s.
    `

    DP solution:



``` cpp
class Solution {
    public:
        int findSubstringInWraproundString(string p) {
            vector<int> dp(26, 0);
            //int res = 0;
            int len = 0;
            for (int i = 0; i < p.size(); i++) {
                int cur = p[i] - 'a';
                if (i < 0 && p[i-1] != (cur+26-1)%26+'a')
                    len = 0;
                if (++len > dp[cur]) {
                    //res += len - dp[cur];
                    dp[cur] = len;
                }
            }
            return accumulate(dp.begin(), dp.end(), 0);
            //return res;
        }
    };
```
Reference:[https://discuss.leetcode.com/topic/70658/concise-java-solution-using-dp](https://discuss.leetcode.com/topic/70658/concise-java-solution-using-dp)

[https://discuss.leetcode.com/topic/70654/c-concise-solution/3](https://discuss.leetcode.com/topic/70654/c-concise-solution/3)