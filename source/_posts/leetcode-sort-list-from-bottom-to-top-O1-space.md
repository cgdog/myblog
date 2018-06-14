---
title: leetCode Sort List自底向上的归并排序 O(1)空间复杂度
id: 364
categories:
  - algorithm
date: 2016-09-14 09:41:18
tags:
  - leetcode
---

[Sort List](https://leetcode.com/problems/sort-list/). Sort a linked list in O(n log n) time using constant space complexity.



``` cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* split(ListNode* head, int n) {
        if (head == NULL) {
            return NULL;
        }
        for (int i = 1; head && i < n; head = head->next, i++);
        if (!head) {
            return NULL;
        }
        ListNode* next = head->next;
        head->next = NULL;
        return next;
    }

    ListNode* merge(ListNode* left, ListNode* right, ListNode* head) {
        ListNode* cur = head;
        while (left && right) {
            if (left->val < right->val) {
                cur->next = left;
                left = left->next;
            } else {
                cur->next = right;
                right = right->next;
            }
            cur = cur->next;
        }

        cur->next = (left ? left : right);
        for (; cur->next; cur = cur->next);
        return cur;
    }

    ListNode* sortList(ListNode* head) {
        if (head == NULL || head->next == NULL) {
            return head;
        }

        ListNode* cur = head;
        int len = 0;
        for (;cur;len++, cur=cur->next);

        ListNode nh(0);
        ListNode* h = &nh;
        h->next = head;
        ListNode* left,*right,*tail;

        for (int step = 1; step < len; step <<= 1) {
            cur = h->next;
            tail = h;
            while (cur) {
                left = cur;
                right = split(left, step);
                cur = split(right, step);
                tail = merge(left, right, tail);
            }
        }
        return h->next;
    }
};
```

> [https://discuss.leetcode.com/topic/10382/bottom-to-up-not-recurring-with-o-1-space-complextity-and-o-nlgn-time-complextity/2](https://discuss.leetcode.com/topic/10382/bottom-to-up-not-recurring-with-o-1-space-complextity-and-o-nlgn-time-complextity/2)
>   [自底向上的归并排序](http://blog.csdn.net/cjf_iceking/article/details/7920153)