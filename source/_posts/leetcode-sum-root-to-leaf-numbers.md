---
title: leetCode Sum Root to Leaf Numbers
id: 646
categories:
date: 2016-10-26 22:36:47
tags:
---

# [Sum Root to Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers/)

Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path 1->2->3 which represents the number 123.

Find the total sum of all root-to-leaf numbers.

For example,

<pre>
    1
   / \
  2   3
</pre>

The root-to-leaf path 1->2 represents the number 12.
The root-to-leaf path 1->3 represents the number 13.

Return the sum = 12 + 13 = 25.

## Solution one (recursive):



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
    int s = 0;
    int helper(TreeNode* root, int tmps) {
        if (root) {
            tmps = tmps * 10 + root->val;
            if (!root->left && !root->right) {
                s += tmps;
            } else {
                if (root->left)
                    helper(root->left, tmps);
                if (root->right)
                    helper(root->right, tmps);
            }
        }
        return s;
    }
    int sumNumbers(TreeNode* root) {

        return helper(root, 0);
    }
};
```

## Solution two (O(1) space Morris traversal):



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

    int sumNumbers(TreeNode* root) {
        int s = 0;
        TreeNode *cur = root, *prev = NULL;
        while (cur != NULL)
        {
            if (cur->left == NULL)
            {
                if (cur->right) cur->right->val = cur->right->val + cur->val * 10;
                if (!cur->left && !cur->right)
                    s += cur->val;
                cur = cur->right;
            }
            else
            {
                prev = cur->left;
                while (prev->right != NULL && prev->right != cur)
                    prev = prev->right;

                if (prev->right == NULL)
                {
                    if (cur->right) cur->right->val = cur->right->val + cur->val * 10;
                    if (cur->left) cur->left->val = cur->left->val + cur->val * 10;

                    cout << cur->val << " ";
                    prev->right = cur;
                    cur = cur->left;
                }
                else
                {
                    if (!prev->left)
                        s += prev->val;
                    prev->right = NULL;
                    cur = cur->right;
                }
            }
        }
        return s;
    }
};
```