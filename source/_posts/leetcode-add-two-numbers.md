---
title: 'leetcode: Add Two Numbers'
id: 299
categories:
  - algorithm
date: 2016-07-10 14:32:49
tags:
  - leetcode
---

## Add Two Numbers

You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

**Input**: (2 -> 4 -> 3) + (5 -> 6 -> 4)

**Output**: 7 -> 0 -> 8

C++代码：



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

     ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {

        ListNode* resList = NULL;
        ListNode* tail = NULL;

        int carry = 0;
        while (l1 != NULL || l2 != NULL)
        {
            int l1V = 0;
            int l2V = 0;
            if (l1 != NULL)
            {
                l1V = l1->val;
                l1 = l1->next;
            }

            if (l2 != NULL)
            {
                l2V = l2->val;
                l2 = l2->next;
            }

            int num = l1V + l2V +carry;

            ListNode * numNode = NULL;

            int newNum = num % 10;
            numNode = new ListNode(newNum);
            if (resList == NULL)
            {
                resList = tail = numNode;
            } else
            {
                tail->next = numNode;
                tail = numNode;
            }
            carry = num / 10;

            if ((l1 == NULL && l2 == NULL) && carry > 0)
            {
                ListNode* tmpNode = new ListNode(carry);
                tail->next = tmpNode;
                tail = tmpNode;
            }
        }

        return resList;
    }
};
```