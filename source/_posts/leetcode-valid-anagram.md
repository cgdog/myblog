---
title: 'leetcode: Valid Anagram'
id: 326
categories:
  - algorithm
date: 2016-07-14 19:55:25
tags:
---


Given two strings s and t, write a function to determine if t is an anagram of s.

For example, s = "anagram", t = "nagaram", return true. s = "rat", t = "car", return false.

Note: You may assume the string contains only lowercase alphabets.

Follow up: What if the inputs contain unicode characters? How would you adapt your solution to such case?

C++实现：



``` cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        int arr[26] = {0};

        for (int i = 0; i &lt; s.size(); i++) {
            arr[s[i]-'a'] += 1;
        }

        for (int i = 0; i &lt; t.size(); i++) {
            arr[t[i]-'a'] -= 1;
        }

        for (int i = 0; i &lt; 26; i++) {
            if (arr[i] != 0) {
                return false;
            }
        }

        return true;
    }
};
```

> 参考：[http://www.cnblogs.com/sherylwang/p/5621595.html](http://www.cnblogs.com/sherylwang/p/5621595.html)