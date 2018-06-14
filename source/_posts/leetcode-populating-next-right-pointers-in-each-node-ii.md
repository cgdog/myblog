---
title: leetCode Populating Next Right Pointers in Each Node II
id: 602
categories:
  - algorithm
date: 2016-10-11 00:05:58
tags:
  - leetcode
  - levelTraversal
---

[Populating Next Right Pointers in Each Node II](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

**Note:**

You may only use constant extra space.

For example,

Given the following binary tree,

<pre>
         1
       /  \
      2    3
     / \    \
    4   5    7
</pre>

After calling your function, the tree should look like:

<pre>
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL
</pre>

**Solution:**



``` cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        TreeLinkNode* head = NULL, *pre = NULL, *cur = root;
        while (cur) {
            while (cur) {
                if (cur->left) {
                    if (pre) {
                        pre->next = cur->left;
                    } else {
                        head = cur->left;
                    }
                    pre = cur->left;
                }

                if (cur->right) {
                    if (pre) {
                        pre->next = cur->right;
                    } else {
                        head = cur->right;
                    }
                    pre = cur->right;
                }
                cur = cur->next;
            }
            cur = head;
            pre = NULL;
            head = NULL;
        }
    }
};
```

> [https://discuss.leetcode.com/topic/1106/o-1-space-o-n-complexity-iterative-solution](https://discuss.leetcode.com/topic/1106/o-1-space-o-n-complexity-iterative-solution)