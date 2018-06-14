---
title: leetcode 472. Concatenated Words
id: 795
categories:
  - algorithm
date: 2017-01-17 16:59:15
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[472\. Concatenated Words](https://leetcode.com/problems/concatenated-words/)

Given a list of words (without duplicates), please write a program that returns all concatenated words in the given list of words.

A concatenated word is defined as a string that is comprised entirely of at least two shorter words in the given array.

**Example:**

    Input: ["cat","cats","catsdogcats","dog","dogcatsdog","hippopotamuses","rat","ratcatdogcat"]

    Output: ["catsdogcats","dogcatsdog","ratcatdogcat"]

    Explanation: "catsdogcats" can be concatenated by "cats", "dog" and "cats"; 
     "dogcatsdog" can be concatenated by "dog", "cats" and "dog"; 
    "ratcatdogcat" can be concatenated by "rat", "cat", "dog" and "cat".

**Note:**

1.  The number of elements of the given array will not exceed 10,000   
2.  The length sum of elements in the given array will not exceed 600,000.  
3.  All the input string will only include lower case letters.  
4.  The returned elements order does not matter.  

DP solution:



``` cpp
class Solution {
public:

    bool canform(string s, unordered_set<string>& prewords) {
        if (prewords.empty()) {
            return false;
        }
        vector<bool> dp(s.length()+1, false);
        dp[0] = true;
        for (int i = 1; i <= s.length(); i++) {
            for (int j = 0; j < i; j++) {
                if (!dp[j]) continue;
                if (prewords.find(s.substr(j,i-j)) != prewords.end()) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }
    vector<string> findAllConcatenatedWordsInADict(vector<string>& words) {
        sort(words.begin(), words.end(), [](const string& a, const string& b)->bool{ return a.length() < b.length();});
        vector<string> res;
        unordered_set<string> prewords;
        for (int i = 0; i < words.size(); i++) {
            if (canform(words[i], prewords)) {
                res.push_back(words[i]);
            }
            prewords.insert(words[i]);
        }
        return res;
    }
};
```

Reference:[https://discuss.leetcode.com/topic/72113/java-dp-solution](https://discuss.leetcode.com/topic/72113/java-dp-solution)