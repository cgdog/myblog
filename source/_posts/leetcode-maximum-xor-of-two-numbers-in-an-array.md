---
title: leetCode Maximum XOR of Two Numbers in an Array
id: 742
categories:
  - algorithm
date: 2016-12-15 20:34:11
tags:
  - C++
  - leetcode
---

[Maximum XOR of Two Numbers in an Array](https://leetcode.com/problems/maximum-xor-of-two-numbers-in-an-array/)

Given a non-empty array of numbers, $a_0, a_1, a_2, … , a_{n-1}$, where $0 ≤ a_i < 2^{31}$.

Find the maximum result of $a_i$ XOR $a_j$, where 0 ≤ i, j < n.

Could you do this in O(n) runtime?

Example:

```
Input: [3, 10, 5, 25, 2, 8]

Output: 28

Explanation: The maximum result is 5 ^ 25 = 28.
```



``` cpp
class Solution {
public:
    int findMaximumXOR(vector<int>& nums) {
        int res = 0, mask = 0;
        unordered_set<int> s;
        for (int i = 31; i >= 0; i--) {
            mask |= (1 << i);
            s.clear();
            for (int j = 0; j < nums.size(); j++) {
                s.insert(nums[j] & mask);
            }
            int possible_new_res = res | (1 << i);
            for (unordered_set<int>::iterator iter = s.begin(); iter != s.end(); iter++) {
                if (s.find(*iter ^ possible_new_res) != s.end()) {
                    res = possible_new_res;
                    break;
                }
            }
        }
        return res;
    }
};
```

Reference:

[https://discuss.leetcode.com/topic/63213/java-o-n-solution-using-bit-manipulation-and-hashmap/18](https://discuss.leetcode.com/topic/63213/java-o-n-solution-using-bit-manipulation-and-hashmap/18)

[https://discuss.leetcode.com/topic/63213/java-o-n-solution-using-bit-manipulation-and-hashmap/17](https://discuss.leetcode.com/topic/63213/java-o-n-solution-using-bit-manipulation-and-hashmap/17)