---
title: leetCode Symmetric Tree
id: 549
categories:
  - algorithm
date: 2016-09-29 18:20:59
tags:
  - leetcode
  - Tree
---

[Symmetric Tree](https://leetcode.com/problems/symmetric-tree/)

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

<pre>
    1
   / \
  2   2
 / \ / \
3  4 4  3
</pre>

But the following `[1,2,2,null,3,null,3]` is not:

<pre>
    1
   / \
  2   2
   \   \
   3    3
</pre>

**Note:**

Bonus points if you could solve it both recursively and iteratively.

### Solution 1: recursively preOrder traversal C++



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

    bool helper(TreeNode* ltree, TreeNode* rtree) {
        if (ltree == NULL && rtree == NULL) {
            return true;
        } else if (ltree && rtree && ltree->val == rtree->val) {
            return helper(ltree->left, rtree->right) && helper(ltree->right, rtree->left);
        } else {
            return false;
        }
    }
    bool isSymmetric(TreeNode* root) {
        if (!root) {
            return true;
        }
        return helper(root->left, root->right);
    }
};
```

### Solution 2: preOrder traversal using two stacks C++. O(n) space



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

    bool isSymmetric(TreeNode* root) {
        if (!root) {
            return true;
        }

        TreeNode* cur1 = root->left, *cur2 = root->right;
        stack&lt;TreeNode*> st1;
        stack&lt;TreeNode*> st2;
        while ((!st1.empty() && !st2.empty()) || (cur1 && cur2))
        {
            while (cur1 && cur2 && cur1->val == cur2->val) {
                st1.push(cur1);
                st2.push(cur2);
                cur1 = cur1->left;
                cur2 = cur2->right;
            }

            if (cur1 == NULL && cur2 == NULL) {
                cur1 = st1.top();
                st1.pop();
                cur1 = cur1->right;
                cur2 = st2.top();
                st2.pop();
                cur2 = cur2->left;
            } else {
                return false;
            }
        }
        return st1.empty() && st2.empty() && !cur1 && !cur2 ;
    }
};
```

### using Morris Traversal. Using O(1) space.

```
// The code is writing..
```