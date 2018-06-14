---
title: 'leetcode: Palindrome Numbe'
id: 309
categories:
  - algorithm
date: 2016-07-13 20:39:08
tags:
  - leetcode
---

Determine whether an integer is a palindrome. Do this without extra space.

c++实现：



``` cpp
class Solution {
public:
    bool isPalindrome(int x) {

        if (x < 0) {
            return false;
        }
        int div=1;
        while (x / div >= 10) {
            div = div * 10;
        }

        while (x != 0) {
            int left = x % 10;
            int right = x / div;
            if (left != right) {
                return false;
            }

            x = (x % div)/10;
            div /= 100;
        }

        return true;
    }
};
```

> 参考:[http://www.cnblogs.com/programnote/p/4691476.html](http://www.cnblogs.com/programnote/p/4691476.html)