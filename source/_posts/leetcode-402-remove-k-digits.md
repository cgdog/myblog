---
title: leetCode 402. Remove K Digits
tags:
  - leetcode
  - stack
id: 669
categories:
  - algorithm
date: 2016-11-07 22:37:40
---

# [402\. Remove K Digits](https://leetcode.com/problems/remove-k-digits/)

Given a non-negative integer num represented as a string, remove k digits from the number so that the new number is the smallest possible.

**Note:**

    The length of num is less than 10002 and will be ≥ k.
    The given num does not contain any leading zero.
    `</pre>

    **Example 1:**

    <pre>`Input: num = "1432219", k = 3
    Output: "1219"
    Explanation: Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.
    `</pre>

    **Example 2:**

    <pre>`Input: num = "10200", k = 1
    Output: "200"
    Explanation: Remove the leading 1 and the number is 200\. Note that the output must not contain leading zeroes.
    `</pre>

    **Example 3:**

```
Input: num = "10", k = 2
    Output: "0"
    Explanation: Remove all the digits from the number and it is left with nothing which is 0.
```


``` cpp
    class Solution {
    public:
        string removeKdigits(string num, int k) {
            int n = num.size();
            if (n == k) return "0";
            stack&lt;char&gt; st;
            int i = 0;
            while (i &lt; n) {
                while (k &gt; 0 &amp;&amp; !st.empty() &amp;&amp; st.top() &gt; num[i]) {
                    st.pop();
                    k--;
                }
                st.push(num[i]);
                i++;
            }
            while (k &gt; 0) {
                st.pop();
                k--;
            }
            string res = "";
            while (!st.empty()) {
                res += st.top();
                st.pop();
            }
            reverse(res.begin(), res.end());
            while (res[0] == '0' &amp;&amp; res.size() &gt; 1) {
                res = res.substr(1);
            }
            return res;
        }
    };
```