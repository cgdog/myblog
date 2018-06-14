---
title: leetCode Flatten Binary Tree to Linked List
id: 584
categories:
  - algorithm
date: 2016-09-30 20:21:12
tags:
  - DFS
  - leetcode
  - Tree
---

# [Flatten Binary Tree to Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)

Given a binary tree, flatten it to a linked list in-place.

For example,

Given

<pre>
         1
        / \
       2   5
      / \   \
     3   4   6
</pre>

The flattened tree should look like:

<pre>
   1
    \
     2
      \
       3
        \
         4
          \
           5
            \
             6
</pre>

**Hints:**

If you notice carefully in the flattened tree, each node's right child points to the next node of a pre-order traversal.

### Solution 1: (recursively) 6ms



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

    void flatten(TreeNode* root) {
        if (root) {
            flatten(root->left);
            flatten(root->right);
            TreeNode* left = root->left;
            TreeNode* right = root->right;
            root->left = NULL;
            if (left) {
                root->right = left;
                TreeNode* tmp = left;
                while (tmp && tmp->right) tmp = tmp->right;
                tmp->right = right;
            }
        }
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/61011/simple-intuitive-java-solution](https://discuss.leetcode.com/topic/61011/simple-intuitive-java-solution)

### Solution 2: (non-recursively) 12ms



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

    void flatten(TreeNode* root) {
        TreeNode* cur = root;
        while (cur) {
            if (cur->left) {
                TreeNode* pre = cur->left;
                while (pre->right) pre = pre->right;
                pre->right = cur->right;
                cur->right = cur->left;
                cur->left = NULL;
            }
            cur = cur->right;
        }
    }
};
```

> Reference:[https://discuss.leetcode.com/topic/3995/share-my-simple-non-recursive-solution-o-1-space-complexity](https://discuss.leetcode.com/topic/3995/share-my-simple-non-recursive-solution-o-1-space-complexity)