---
title: leetCode Construct Binary Tree from Inorder and Postorder Traversal
id: 560
categories:
  - algorithm
date: 2016-09-29 23:47:37
tags:
  - leetcode
  - Tree
---

[Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

Given inorder and postorder traversal of a tree, construct the binary tree.

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

    void buildTree(TreeNode* & root, vector<int>& inorder, vector<int>& postorder, int l1, int r1, int l2, int r2) {
        root = new TreeNode(postorder[r2]);
        if (l1 < r1) {
            int pos = l1;
            for (; pos <= r1; pos++) {
                if (inorder[pos] == postorder[r2]) {
                    break;
                }
            }
            if (pos > l1) {
                // using buildTree(root->left, inorder, postorder, l1, pos-1, l2, l2+(pos-l1)); It will be wrong!
                buildTree(root->left, inorder, postorder, l1, pos-1, l2, l2+(pos-l1-1));
            }
            if (pos < r1) {
                // using buildTree(root->left, inorder, postorder, l1, pos-1, l2, l2+(pos-l1)+1); It will be wrong!
                buildTree(root->right, inorder, postorder, pos+1, r1, l2+(pos-l1), r2-1);
            }
        }
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        if (inorder.size() == 0) {
            return NULL;
        }
        TreeNode* root = NULL;
        buildTree(root, inorder, postorder, 0, inorder.size()-1, 0, postorder.size()-1);
        return root;
    }
};
```

有一个迭代方法见：[https://discuss.leetcode.com/topic/4746/my-comprehension-of-o-n-solution-from-hongzhi](https://discuss.leetcode.com/topic/4746/my-comprehension-of-o-n-solution-from-hongzhi)