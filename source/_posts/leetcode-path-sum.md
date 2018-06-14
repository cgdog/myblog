---
title: leetCode Path Sum
id: 580
categories:
  - 未分类
date: 2016-09-30 16:32:07
tags:
---

# [Path Sum](https://leetcode.com/problems/path-sum/)

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

For example:

Given the below binary tree and `sum = 22`,

<pre>
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
</pre>

return true, as there exist a root-to-leaf path `5-&gt;4-&gt;11-&gt;2` which sum is 22.



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

    bool helper(TreeNode* root, int & sumtmp, const int sum) {
        if (root == NULL) {
            return false;
        }
        sumtmp = sumtmp+root->val;
        if (root->left == NULL && root->right == NULL) {
            return sumtmp == sum;
        } else if (root->left && root->right == NULL) {
            return helper(root->left, sumtmp, sum);
        } else if (root->left == NULL && root->right) {
            return helper(root->right, sumtmp, sum);
        } else {
            int tmp = sumtmp;
            return helper(root->left, sumtmp, sum) || helper(root->right, tmp, sum);
        }
    }
    bool hasPathSum(TreeNode* root, int sum) {

        int sumtmp = 0;
        return helper(root, sumtmp, sum);
    }
};
```