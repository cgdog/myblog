---
title: 'leetcode: Roman to Intege'
id: 311
categories:
  - algorithm
date: 2016-07-13 22:19:30
tags:
  - leetcode
---

# Roman to Intege

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.



``` cpp
class Solution {
public:

    int valueOf(char ch) {
        switch (ch) {
            case 'I': return 1;
            case 'V': return 5;
            case 'X': return 10;
            case 'C': return 100;
            case 'L': return 50;
            case 'D': return 500;
            case 'M': return 1000;

            default : return 0;
        }
    }
    int romanToInt(string s) {

        int res = 0;
        for (int i = 0; i < s.size(); i++) {
            int num = valueOf(s[i]);
            if (num == 0)
                return 0;
            int nextNum = 0;
            if (i + 1 < s.size()) {
                nextNum = valueOf(s[i+1]);
            }
            if (num >= nextNum) {
                res += num;
            } else {
                res -= num;
            }
        }

        return res;
    }
};
```

> 参考：[http://zhidao.baidu.com/question/42592740.html](http://zhidao.baidu.com/question/42592740.html)
>   [http://outofmemory.cn/code-snippet/6988/C-jiang-luoma-number-turn-huancheng-ala-bo-number](http://outofmemory.cn/code-snippet/6988/C-jiang-luoma-number-turn-huancheng-ala-bo-number)