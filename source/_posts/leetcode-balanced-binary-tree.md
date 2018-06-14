---
title: leetCode Balanced Binary Tree
id: 576
categories:
  - algorithm
date: 2016-09-30 15:25:08
tags:
  - DFS
  - leetcode
  - Tree
---

[Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.


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
    bool isBalanced(TreeNode* root, int & height) {
        if (root == NULL) {
            height = 0;
            return true;
        }
        int leftH, rightH;
        bool isLeft, isRight;
        isLeft = isBalanced(root->left, leftH);
        isRight = isBalanced(root->right, rightH);
        height = max(leftH, rightH) + 1;
        return isLeft && isRight && (abs(leftH - rightH) <= 1);
    }
    bool isBalanced(TreeNode* root) {
        int height;
        return isBalanced(root, height);
    }
};
```