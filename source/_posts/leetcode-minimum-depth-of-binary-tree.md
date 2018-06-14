---
title: leetCode Minimum Depth of Binary Tree
id: 578
categories:
  - algorithm
date: 2016-09-30 15:35:50
tags:
  - DFS
  - leetcode
  - Tree
---

[Minimum Depth of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.



``` cpp
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
    int minDepth(TreeNode* root) {
        if (root == NULL) {
            return 0;
        }
        if (root->left == NULL && root->right == NULL) {
            return 1;
        } else if (root->left && root->right == NULL) {
            return minDepth(root->left)+1;
        } else if (root->left == NULL && root->right) {
            return minDepth(root->right)+1;
        } else {
            int left = minDepth(root->left);
            int right = minDepth(root->right);
            return min(left, right)+1;
        }
    }
};
```