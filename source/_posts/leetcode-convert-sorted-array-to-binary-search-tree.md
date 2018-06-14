---
title: leetCode Convert Sorted Array to Binary Search Tree
id: 573
categories:
  - algorithm
date: 2016-09-30 14:30:17
tags:
  - leetcode
  - Tree
---

[Convert Sorted Array to Binary Search Tree](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.


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

    TreeNode* sortedArrayToBST(vector&lt;int>& nums, int start, int end) {
        TreeNode* root = new TreeNode(nums[(start+end)/2]);
        if (start &lt; (start+end)/2) {
            root->left = sortedArrayToBST(nums, start, (start+end)/2-1);
        }
        if ((start+end)/2 &lt; end) {
            root->right = sortedArrayToBST(nums, (start+end)/2+1, end);
        }
        return root;
    }
    TreeNode* sortedArrayToBST(vector&lt;int>& nums) {
        if (nums.size() == 0) {
            return NULL;
        }
        TreeNode* root = sortedArrayToBST(nums, 0, nums.size()-1);
        return root;
    }
};
```