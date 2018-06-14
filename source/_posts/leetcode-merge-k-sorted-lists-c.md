---
title: leetcode Merge k Sorted Lists c++
id: 366
categories:
  - algorithm
date: 2016-09-14 10:59:45
tags:
  - leetcode
---

[Merge k Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.



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
    ListNode* merge(ListNode* l1, ListNode* l2) {
        if (!l1) {
            return l2;
        }
        if (!l2) {
            return l1;
        }

        ListNode nh(0);
        ListNode *h = &nh;
        while (l1 && l2) {
            if (l1->val &lt; l2->val) {
                h->next = l1;
                l1 = l1->next;
            } else {
                h->next = l2;
                l2 = l2->next;
            }
            h = h->next;
        }
        h->next = (l1 ? l1 : l2);
        return nh.next;
    }
    ListNode* mergeKLists(vector&lt;ListNode*>& lists) {
        if (lists.size() == 0) {
            return NULL;
        } 
        ListNode nh(0);
        ListNode *h = &nh;

        while (lists.size() > 1) {

            lists.push_back(merge(lists[0], lists[1]));
            lists.erase(lists.begin());
            lists.erase(lists.begin());
        }

        return lists[0];
    }
};
```

> [https://discuss.leetcode.com/topic/6882/sharing-my-straightforward-c-solution-without-data-structure-other-than-vector](https://discuss.leetcode.com/topic/6882/sharing-my-straightforward-c-solution-without-data-structure-other-than-vector)