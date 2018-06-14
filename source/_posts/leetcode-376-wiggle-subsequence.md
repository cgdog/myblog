---
title: leetCode 376. Wiggle Subsequence
id: 778
categories:
  - algorithm
date: 2017-01-05 11:47:55
tags:
  - Dynamic programming
  - leetcode
---

[376\. Wiggle Subsequence](https://leetcode.com/problems/wiggle-subsequence/)

A sequence of numbers is called a wiggle sequence if the differences between successive numbers strictly alternate between positive and negative. The first difference (if one exists) may be either positive or negative. A sequence with fewer than two elements is trivially a wiggle sequence.

For example, [1,7,4,9,2,5] is a wiggle sequence because the differences (6,-3,5,-7,3) are alternately positive and negative. In contrast, [1,4,7,2,5] and [1,7,4,5,5] are not wiggle sequences, the first because its first two differences are positive and the second because its last difference is zero.

Given a sequence of integers, return the length of the longest subsequence that is a wiggle sequence. A subsequence is obtained by deleting some number of elements (eventually, also zero) from the original sequence, leaving the remaining elements in their original order.

Examples:

    Input: [1,7,4,9,2,5]
    Output: 6
    The entire sequence is a wiggle sequence.

    Input: [1,17,5,10,13,15,10,5,16,8]
    Output: 7
    There are several subsequences that achieve this length. One is [1,17,10,13,10,16,8].

    Input: [1,2,3,4,5,6,7,8,9]
    Output: 2

Follow up:

Can you do it in O(n) time?

My naive O(n) time solution:



``` cpp
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        int n = nums.size();
        if (n < 1) return 0;
        if (n == 1) return 1;
        vector<int> diffs(nums.size()-1);
        int siz = 0;
        for (int i = 1; i < n; i++) {
            int tmp = nums[i]-nums[i-1];
            if (tmp != 0)
                diffs[siz++] = tmp;
        }
        if (siz == 0) return 1;
        int count = 1;
        int pre = diffs[0];
        for (int i = 1; i < siz; i++) {
            if (diffs[i]*pre < 0)
            {
                count++;
                pre = diffs[i];
            }
        }
        return count+1;
    }
};
```

DB solution:
[https://discuss.leetcode.com/topic/51893/two-solutions-one-is-dp-the-other-is-greedy-8-lines](https://discuss.leetcode.com/topic/51893/two-solutions-one-is-dp-the-other-is-greedy-8-lines)

Another solution that can preserve the Wiggle sequence with maximum length:

[https://discuss.leetcode.com/topic/51946/very-simple-java-solution-with-detail-explanation](https://discuss.leetcode.com/topic/51946/very-simple-java-solution-with-detail-explanation)