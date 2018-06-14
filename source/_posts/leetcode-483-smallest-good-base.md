---
title: leetcode 483. Smallest Good Base
id: 828
categories:
  - algorithm
date: 2017-02-12 16:48:46
tags:
  - leetcode
  - math
---

[483\. Smallest Good Base](https://leetcode.com/problems/smallest-good-base/)

For an integer n, we call k>=2 a good base of n, if all digits of n base k are 1.

Now given a string representing n, you should return the smallest good base of n in string format.

**Example 1:**

    Input: "13"
    Output: "3"
    Explanation: 13 base 3 is 111.
    `

    **Example 2:**

    `Input: "4681"
    Output: "8"
    Explanation: 4681 base 8 is 11111.
    `

    **Example 3:**

    Input: "1000000000000000000"
    Output: "999999999999999999"
    Explanation: 1000000000000000000 base 999999999999999999 is 11.

**Note:**

1\. The range of n is [3, 10^18].

2\. The string representing n is always valid and will not have leading zeros.



``` cpp
class Solution {
public:
    string smallestGoodBase(string n) {
        typedef unsigned long long ull;
        ull num = (ull)stoll(n);
        int maxlen = log(num)/log(2) + 1;
        for (int i = maxlen; i >= 3; i--) {
            ull b = (ull)pow(num, 1.0/(i-1));
            ull sum = 1, cur = 1;
            for (int j = 1; j < i; j++) {
                cur *= b;
                sum += cur;
            }
            if (sum == num) {
                return to_string(b);
            }
        }
        return to_string(num-1);
    }
};
```

Reference: [https://discuss.leetcode.com/topic/76347/3ms-ac-c-long-long-int-binary-search/2](https://discuss.leetcode.com/topic/76347/3ms-ac-c-long-long-int-binary-search/2)