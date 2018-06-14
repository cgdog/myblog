---
title: leetCode Count Complete Tree Nodes
id: 386
categories:
  - algorithm
date: 2016-09-16 16:24:36
tags:
  - leetcode
---

[Count Complete Tree Nodes](https://leetcode.com/problems/count-complete-tree-nodes/)

Given a complete binary tree, count the number of nodes.

Definition of a complete binary tree from Wikipedia:

In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.



``` cpp
// 26 ms

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int countNodes(TreeNode* root) {
        int num = 0;
        if (root) {
            TreeNode *left = root, *right = root;
            int numl = 0, numr = 0;
            while (left) {
                numl++;
                left = left->left;
            }
            while (right) {
                numr++;
                right = right->right;
            }
            if (numl == numr) {
                num = pow(2, numl)-1;
            } else {
                num = 1 + countNodes(root->left) + countNodes(root->right);
            }
        }
        return num;
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/15515/easy-short-c-recursive-solution/6](https://discuss.leetcode.com/topic/15515/easy-short-c-recursive-solution/6)