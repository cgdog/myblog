---
title: 'leetcode: Integer to Roman'
id: 313
categories:
  - algorithm
date: 2016-07-13 22:46:13
tags:
  - leetcode
---


Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.

C++实现



``` cpp
class Solution {
public:
    string intToRoman(int num) {

        string romanChar[][10] = {
            { "", "I", "II", "III", "IV", "V", "VI", "VII", "VIII", "IX" },
            { "", "X", "XX", "XXX", "XL", "L", "LX", "LXX", "LXXX", "XC" },
            { "", "C", "CC", "CCC", "CD", "D", "DC", "DCC", "DCCC", "CM" },
            { "", "M", "MM", "MMM", "", "", "", "", "", "" }
        };

        return romanChar[3][num / 1000]+
        romanChar[2][num%1000/100]+
        romanChar[1][num%100/10]+
        romanChar[0][num%10];
    }
};
```

> 参考：[http://my.oschina.net/Tsybius2014/blog/486752](http://my.oschina.net/Tsybius2014/blog/486752)