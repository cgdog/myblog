---
title: 'leetcode: Reverse Integer'
id: 301
categories:
  - algorithm
date: 2016-07-10 15:10:45
tags:
  - leetcode
---

Reverse Integer

Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

> **Hint**:Have you thought about this?
> 
> Here are some good questions to ask before coding. Bonus points for you if you have already thought through this!
> 
> If the integer's last digit is 0, what should the output be? ie, cases such as 10, 100.
> 
> Did you notice that the reversed integer might overflow? Assume the input is a 32-bit integer, then the reverse of 1000000003 overflows. How should you handle such cases?
> 
> For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.



``` cpp
class Solution {
public:
    int reverse(int x) {

        string maxIntStr = "2147483647";// INT_MAX
        string reversedNumStr = ""; // 用于判断反转后的整数是否溢出

        int y=(x<0)?-x:x;

        int res = 0;

        if (y>=0 && y <= 9) {
            res = y;
            reversedNumStr += y+'0';
        } else {
            while (y>0) {
                reversedNumStr += y % 10 + '0';
                res = res *10 + y % 10;
                y /= 10;
            }
        }

        if (reversedNumStr.size() >= maxIntStr.size()) {// 有溢出的可能
            if (reversedNumStr.compare(maxIntStr) > 0) {// 溢出了，返回0
                return 0;
            }
        }
        res = (x < 0)?-res:res;

        return res;
    }
};
```