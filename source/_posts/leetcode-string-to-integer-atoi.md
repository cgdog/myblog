---
title: 'leetcode: String to Integer (atoi)'
id: 303
categories:
  - algorithm
date: 2016-07-13 19:26:01
tags:
  - leetcode
---

Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

Update (2015-02-10): The signature of the C++ function had been updated. If you still see your function signature accepts a const char * argument, please click the reload button to reset your code definition.

spoilers alert... click to show requirements for atoi.

Requirements for atoi: The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, INT_MAX (2147483647) or INT_MIN (-2147483648) is returned.

C++实现：



``` cpp
class Solution {
public:
    int myAtoi(string str) {

        if (str.compare("") == 0 || str.compare("-") ==0 || str.compare("+")==0) {
            return 0;
        }

        // 去除开头的空格
        while (str[0] == ' ') {
            str = str.substr(1);
        }

        string maxIntStr = "2147483647";// INT_MAX
        string minIntStr = "2147483648";// INT_MIN

        string numStr = str;
        // 去除开头的正负号
        if (str[0] == '-' || str[0] == '+') {
            numStr = str.substr(1);
        }
        // 若仍有正负号，不符合要求，直接返回0
        if (numStr[0] == '-' || numStr[0] == '+') {
            return 0;
        }

        int num = 0;
        int i;
        for (i = 0; i &lt; numStr.size(); i++) {
            // 遇到非数字字符，中断循环，舍弃后面的字符子串
            if (!(numStr[i]>= '0' && numStr[i] &lt;= '9')) {
                break;
            }
            num = num * 10 + numStr[i] - '0';
        }

        numStr = numStr.substr(0,i);
        // 判断是否有溢出
        if (str[0]=='-') {
            if (i > minIntStr.size() || (i == minIntStr.size() && numStr.compare(minIntStr) > 0)) {
                return INT_MIN;
            }
        } else {
            if (i > maxIntStr.size() || (i == maxIntStr.size() && numStr.compare(maxIntStr) > 0)) {

                return INT_MAX;
            }
        }

        if (str[0] == '-') {
            num = -num;
        }
        return num;
    }
};
```