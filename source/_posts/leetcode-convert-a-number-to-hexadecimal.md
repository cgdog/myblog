---
title: leetCode Convert a Number to Hexadecimal
id: 739
categories:
  - algorithm
date: 2016-12-15 19:28:06
tags:
  - leetcode
---

[Convert a Number to Hexadecimal](https://leetcode.com/problems/convert-a-number-to-hexadecimal/)

Given an integer, write an algorithm to convert it to hexadecimal. For negative integer, two’s complement method is used.

Note:

All letters in hexadecimal (a-f) must be in lowercase. The hexadecimal string must not contain extra leading 0s. If the number is zero, it is represented by a single zero character '0'; otherwise, the first character in the hexadecimal string will not be the zero character. The given number is guaranteed to fit within the range of a 32-bit signed integer. You must not use any method provided by the library which converts/formats the number to hex directly. Example 1:

<pre>Input:
26

Output:
"1a"
</pre>

Example 2:

<pre>Input:
-1

Output:
"ffffffff"
</pre>



``` cpp
class Solution {
public:
    string toHex(int num) {
        if (num == 0) return "0";
        string res("");
        for (int i = 0; i < 8; i++) {
            int tmp = num & 15;
            num = num >> 4;
            if (tmp < 10) {
                res += (char)('0'+tmp);
            } else {
                res += char('a'+(tmp-10));
            }
        }
        reverse(res.begin(), res.end());
        int pos = 0;
        while (res[pos] == '0') {
            pos++;
        }
        return res.substr(pos);
    }
};
```

More concise code:



``` cpp
class Solution {
public:
    string toHex(int num) {
        if (num == 0) return "0";
        string res("");
        for (int i = 0; num && i < 8; i++) {
            int tmp = num & 15;
            num = num >> 4;
            if (tmp < 10) {
                res = (char)('0'+tmp)+res;
            } else {
                res = char('a'+(tmp-10))+res;
            }
        }
        return res;
    }
};
```