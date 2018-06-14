---
title: leetCode Regular Expression Matching
id: 657
categories:
  - algorithm
date: 2016-11-04 09:52:15
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

Implement regular expression matching with support for '.' and '*'.

<pre>'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
</pre>

**recursive and DP solutions**



``` cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        if (p.empty())    return s.empty();

        if ('*' == p[1])
            // x* matches empty string or at least one character: x* -> xx*
            // *s is to ensure s is non-empty
            return (isMatch(s, p.substr(2)) || !s.empty() && (s[0] == p[0] || '.' == p[0]) && isMatch(s.substr(1), p));
        else
            return !s.empty() && (s[0] == p[0] || '.' == p[0]) && isMatch(s.substr(1), p.substr(1));
    }
};

class Solution {
public:
    bool isMatch(string s, string p) {
        /**
         * f[i][j]: if s[0..i-1] matches p[0..j-1]
         * if p[j - 1] != '*'
         *      f[i][j] = f[i - 1][j - 1] && s[i - 1] == p[j - 1]
         * if p[j - 1] == '*', denote p[j - 2] with x
         *      f[i][j] is true iff any of the following is true
         *      1) "x*" repeats 0 time and matches empty: f[i][j - 2]
         *      2) "x*" repeats >= 1 times and matches "x*x": s[i - 1] == x && f[i - 1][j]
         * '.' matches any single character
         */
        int m = s.size(), n = p.size();
        vector&lt;vector&lt;bool>> f(m + 1, vector&lt;bool>(n + 1, false));

        f[0][0] = true;
        for (int i = 1; i &lt;= m; i++)
            f[i][0] = false;
        // p[0.., j - 3, j - 2, j - 1] matches empty iff p[j - 1] is '*' and p[0..j - 3] matches empty
        for (int j = 1; j &lt;= n; j++)
            f[0][j] = j > 1 && '*' == p[j - 1] && f[0][j - 2];

        for (int i = 1; i &lt;= m; i++)
            for (int j = 1; j &lt;= n; j++)
                if (p[j - 1] != '*')
                    f[i][j] = f[i - 1][j - 1] && (s[i - 1] == p[j - 1] || '.' == p[j - 1]);
                else
                    // p[0] cannot be '*' so no need to check "j > 1" here
                    f[i][j] = f[i][j - 2] || (s[i - 1] == p[j - 2] || '.' == p[j - 2]) && f[i - 1][j];

        return f[m][n];
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/6183/my-concise-recursive-and-dp-solutions-with-full-explanation-in-c](https://discuss.leetcode.com/topic/6183/my-concise-recursive-and-dp-solutions-with-full-explanation-in-c)

**backtracking solution**



``` cpp
//regular expression matching
//first solution: using recursive version
class Solution {
public:
    bool isMatch(string s, string p) {
        int m = s.length(), n = p.length();
        return backtracking(s, m, p, n);
    }

    bool backtracking(string& s, int i, string& p, int j) {
        if (i == 0 && j == 0) return true;
        if (i != 0 && j == 0) return false;
        if (i == 0 && j != 0) {
            //in this case only p == "c*c*c*" this pattern can match null string
            if (p[j-1] == '*') {
                return backtracking(s, i, p, j-2);
            }
            return false;
        }
        //now both i and j are not null
        if (s[i-1] == p[j-1] || p[j-1] == '.') {
            return backtracking(s, i - 1, p, j - 1);
        } else if (p[j-1] == '*') {
            //two cases: determines on whether p[j-2] == s[i-1]
            //first p[j-2]* matches zero characters of p
            if (backtracking(s, i, p, j - 2)) return true;
            //second consider whether p[j-2] == s[i-1], if true, then s[i-1] is matched, move to backtracking(i - 1, j)
            if (p[j-2] == s[i-1] || p[j-2] == '.') {
                return backtracking(s, i - 1, p, j);
            }
            return false;
        }
        return false;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/40868/8ms-backtracking-solution-c](https://discuss.leetcode.com/topic/40868/8ms-backtracking-solution-c)