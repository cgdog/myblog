---
title: Binary Tree Maximum Path Sum
id: 604
categories:
  - algorithm
date: 2016-10-11 10:53:11
tags:
  - DFS
  - leetcode
---

[Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/)

Given a binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path does not need to go through the root.

For example:

Given the below binary tree,



```
       1
      / \
     2   3
```


```
Return `6`.
```



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
    int sum = 0;
    int helper(TreeNode* root) {
        if (!root) return 0;
        int left = max(0, helper(root->left));
        int right = max(0, helper(root->right));
        sum = max(sum, left+right+root->val);
        return max(left, right)+root->val;
    }

    int maxPathSum(TreeNode* root) {
        if (root) {
            sum = INT_MIN;
            helper(root);
        }
        return sum;
    }
};
```

> [https://discuss.leetcode.com/topic/4407/accepted-short-solution-in-java](https://discuss.leetcode.com/topic/4407/accepted-short-solution-in-java)