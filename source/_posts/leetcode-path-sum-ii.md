---
title: leetCode Path Sum II
id: 582
categories:
  - algorithm
date: 2016-09-30 17:38:08
tags:
  - backtracking
  - DFS
  - leetcode
  - Tree
---

[Path Sum II](https://leetcode.com/problems/path-sum-ii/)

Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

For example:

Given the below binary tree and sum = 22,

<pre>
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
</pre>

return

<pre>
[
   [5,4,11,2],
   [5,8,4,5]
]
</pre>



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

    void findPaths(TreeNode* root, int sum, vector<int> &path, vector<vector<int>> &res) {
        if (!root) return;
        path.push_back(root->val);
        if (root->left == NULL && root->right == NULL && sum == root->val) {
            res.push_back(path);
        }
        findPaths(root->left, sum - root->val, path, res);
        findPaths(root->right, sum - root->val, path, res);
        path.pop_back();
    }

    vector<vector<int>> pathSum(TreeNode* root, int sum) {
        vector<vector<int>> res;
        vector<int> path;
        findPaths(root, sum, path, res);
        return res;
    }
};
```

Reference:

> *   [https://discuss.leetcode.com/topic/18454/12ms-11-lines-c-solution](https://discuss.leetcode.com/topic/18454/12ms-11-lines-c-solution)