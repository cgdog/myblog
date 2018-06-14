---
title: leetCode Construct Binary Tree from Preorder and Inorder Traversal
id: 556
categories:
  - algorithm
date: 2016-09-29 21:59:53
tags:
  - leetcode
  - Tree
---

# [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

Given preorder and inorder traversal of a tree, construct the binary tree.

**Note:**

You may assume that duplicates do not exist in the tree.



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
    void buildTree(TreeNode*& root, vector<int>& preorder, vector<int>& inorder, int left, int right, int left2, int right2) {
        root = new TreeNode(preorder[left]);
        if (left < right) {

            int pos;
            for (int i = left2; i <= right2; i++) {
                if (inorder[i] == preorder[left]) {
                    pos = i;
                    break;
                }
            }

            if (pos > left2) {
                buildTree(root->left, preorder, inorder, left+1, left+(pos-left2), left2, pos-1);
            }
            if (pos < right2) {
                buildTree(root->right, preorder, inorder, left+(pos-left2)+1, right, pos+1, right2);
            }
        }
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if (preorder.size() == 0) {
            return NULL;
        }
        TreeNode* root = NULL;

        buildTree(root, preorder, inorder, 0, preorder.size()-1,0, inorder.size()-1);
        return root;
    }
};
```