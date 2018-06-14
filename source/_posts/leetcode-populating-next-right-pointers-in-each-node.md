---
title: leetCode Populating Next Right Pointers in Each Node
id: 586
categories:
  - algorithm
date: 2016-09-30 22:29:08
tags:
  - leetcode
  - Tree
---

[Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

Given a binary tree

<pre>
    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }
</pre>

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

**Note:**

> *   You may only use constant extra space.
> *   You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).
> 
>       For example,
> 
>       Given the following perfect binary tree,

<pre>
         1
       /  \
      2    3
     / \  / \
    4  5  6  7
</pre>

After calling your function, the tree should look like:

<pre>
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL
</pre>

**The method below artfully use the next pointer to go through the nodes on the same level.**



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
        if (!root) {
            return;
        }
        while (root->left) {
            TreeLinkNode *p = root;
            while (p) {
                p->left->next = p->right;
                if (p->next) p->right->next = p->next->left;
                p = p->next;
            }
            root = root->left;
        }
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/9579/my-simple-non-iterative-c-code-with-o-1-memory](https://discuss.leetcode.com/topic/9579/my-simple-non-iterative-c-code-with-o-1-memory)