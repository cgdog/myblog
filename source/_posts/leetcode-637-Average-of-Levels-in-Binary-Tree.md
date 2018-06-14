---
title: leetcode-637-Average-of-Levels-in-Binary-Tree
categories:
  - algorithm
date: 2017-07-10 22:02:50
tags:
  - C++
  - leetcode
---

Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.

**Example 1:**


```
Input:
    3
   / \
  9  20
    /  \
   15   7
Output: [3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
```

**Note:**

The range of node's value is in the range of 32-bit signed integer.


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
    vector<double> averageOfLevels(TreeNode* root) {
        queue<TreeNode*> q;
        int next = 0, cur = 0;
        vector<double> res;
        if (!root) {
            return res;
        }
        
        q.push(root);
        cur = 1;
        int bak = cur;
        double sum = 0;
        while (!q.empty()) {
            TreeNode* c = q.front();
            sum += c->val;
            q.pop();
            cur -= 1;
            
            if (c->left) {
                q.push(c->left);
                ++next;
            }
            
            if (c->right) {
                q.push(c->right);
                ++next;
            }
            
            if (cur == 0) {
                res.push_back(sum / bak);
                bak = cur = next;
                next = 0;
                sum = 0;
            }
        }
        return res;
    }
};
```