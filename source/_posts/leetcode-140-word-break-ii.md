---
title: leetcode 140. Word Break II
id: 801
categories:
  - algorithm
date: 2017-01-18 16:05:23
tags:
  - C++
  - DFS
  - Dynamic programming
  - leetcode
---

[140\. Word Break II](https://leetcode.com/problems/word-break-ii/)

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. You may assume the dictionary does not contain duplicate words.

Return all such possible sentences.

For example, given
`s = "catsanddog"`,
`dict = ["cat", "cats", "and", "sand", "dog"]`.

A solution is `["cats and dog", "cat sand dog"]`.

Direct DFS solution (Time Limit Exceeded):



``` cpp
class Solution {
public:
    vector<string> wordBreak(string s, vector<string>& wordDict) {
        vector<string> res;
        unordered_set<string> wordset(wordDict.begin(), wordDict.end());
        DFS(s, wordset, res, "");
        return res;
    }
    void DFS(string s, unordered_set<string>& wordDict, vector<string>& res, string cur_str) {
        if (s.size() == 0) {
            res.push_back(cur_str);
            return;
        }
        for (int i = 1; i <= s.size(); i++) {
            string sub = s.substr(0, i);
            if (wordDict.count(sub)) {
                string tmp = cur_str;
                if (cur_str !="") {
                    cur_str += " ";
                }
                cur_str += sub;
                DFS(s.substr(i), wordDict, res, cur_str);
                cur_str = tmp;
            }
        }
    }
};
```

Solution with cache:



``` cpp
class Solution {
public:
    vector<string> wordBreak(string s, vector<string>& wordDict) {
        unordered_set<string> wordset(wordDict.begin(), wordDict.end());
        unordered_map<string, vector<string>> cache;
        return DFS(s, wordset, cache);
    }
    vector<string> DFS(string s, unordered_set<string>& wordDict, unordered_map<string, vector<string>> &cache) {
        if (cache.count(s)) return cache[s];
        vector<string> res;
        if (wordDict.count(s)) res.push_back(s);

        for (int i = 1; i < s.size(); i++) {
            string sub = s.substr(0, i);
            if (wordDict.count(sub)) {
                string rem = s.substr(i);
                vector<string> rems = DFS(rem, wordDict, cache);
                if (rem.size() > 0) {
                    for (int j = 0; j < rems.size(); j++) {
                        rems[j] = sub+" "+rems[j];
                    }
                    res.insert(res.end(), rems.begin(), rems.end());
                }
            }
        }
        cache[s] = res;
        return res;
    }
};
```

Reference:

[https://discuss.leetcode.com/topic/12997/11ms-c-solution-concise](https://discuss.leetcode.com/topic/12997/11ms-c-solution-concise)

[https://discuss.leetcode.com/topic/27855/my-concise-java-solution-based-on-memorized-dfs](https://discuss.leetcode.com/topic/27855/my-concise-java-solution-based-on-memorized-dfs)