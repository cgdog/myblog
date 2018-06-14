---
title: leetCode Group Anagrams
tags:
  - hashtable
  - leetcode
id: 409
categories:
  - algorithm
date: 2016-09-21 00:00:49
---

[Group Anagrams](https://leetcode.com/problems/anagrams/)

Given an array of strings, group anagrams together.

For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"],

Return:

[

&nbsp;&nbsp;&nbsp;&nbsp;  ["ate", "eat","tea"],

&nbsp;&nbsp;&nbsp;&nbsp;  ["nat","tan"],

&nbsp;&nbsp;&nbsp;&nbsp;  ["bat"]

]

Note: All inputs will be in lower-case.



``` cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        unordered_map<string, vector<string>> m;
        for (int i = 0; i < strs.size(); i++) {
            string key = strs[i];
            sort(key.begin(), key.end());
            if (m.count(key)) {
                m[key].push_back(strs[i]);
            } else {
                vector<string> v;
                v.push_back(strs[i]);
                m[key] = v;
            }
        }
        for (unordered_map<string, vector<string>>::iterator iter = m.begin(); iter != m.end(); iter++) {
            res.push_back(iter->second);
        }
        return res;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/24494/share-my-short-java-solution](https://discuss.leetcode.com/topic/24494/share-my-short-java-solution)