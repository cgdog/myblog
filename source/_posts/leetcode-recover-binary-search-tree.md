---
title: leetCode Recover Binary Search Tree
id: 542
categories:
  - algorithm
date: 2016-09-29 16:40:25
tags:
  - DFS
  - leetcode
  - Tree
---

# [Recover Binary Search Tree](https://leetcode.com/problems/recover-binary-search-tree/)

Two elements of a binary search tree (BST) are swapped by mistake.

Recover the tree without changing its structure.

**Note:**

A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?

### Solution 1: C++ recursive inorder traverse .

Using O(log(n)) space, O(n) time and the worst-case space complexity will become O(n). beats 54.14% of cpp submissions.



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

    void inTraverse(TreeNode* node, TreeNode*& pre, TreeNode* & one, TreeNode* & two) {
        if (node == NULL) {
            return;
        }
        if (node->left) {
            inTraverse(node->left, pre, one, two);
        }
        if (pre != NULL && one == NULL && pre->val >= node->val) {
            one = pre;
        }
        if (one != NULL && pre->val >= node->val) {
            two = node;
        }
        pre = node;
        if (node->right) {
            inTraverse(node->right, pre, one, two);
        }
    }
    void recoverTree(TreeNode* root) {

        TreeNode* pre = NULL, *one = NULL, *two = NULL;
        inTraverse(root, pre, one, two);
        if (one && two) {
            int val = one->val;
            one->val = two->val;
            two->val = val;
        }

    }
};
```

### Solution 2: C++ Morris Traversal.

Using O(1) space, O(n) time.beats 66.30% of cpp submissions.



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

    void recoverTree(TreeNode* root) {

        TreeNode* pre = NULL, *one = NULL, *two = NULL, *cur = root, *prev = NULL;
        while (cur) {
            if (cur->left == NULL) {
                if (prev && prev->val >= cur->val) {
                    if (one == NULL) {
                        one = prev;
                    }
                    two = cur;
                }
                prev = cur;
                cur = cur->right;
            } else {
                pre = cur->left;
                while (pre->right && pre->right != cur) {
                    pre = pre->right;
                }
                if (pre->right == NULL) {
                    pre->right =cur;
                    cur = cur->left;
                } else {
                    pre->right = NULL;
                    if (prev && prev->val >= cur->val) {
                        if (one == NULL) {
                            one = pre;
                        }
                        two = cur;
                    }
                    prev = cur;
                    cur = cur->right;
                }
            }
        }
        if (one && two) {
            int val = one->val;
            one->val = two->val;
            two->val = val;
        }

    }
};
```

**参考：**

> 1.  [https://discuss.leetcode.com/topic/3988/no-fancy-algorithm-just-simple-and-powerful-in-order-traversal](https://discuss.leetcode.com/topic/3988/no-fancy-algorithm-just-simple-and-powerful-in-order-traversal)
> 2.  [https://discuss.leetcode.com/topic/29161/share-my-solutions-and-detailed-explanation-with-recursive-iterative-in-order-traversal-and-morris-traversal](https://discuss.leetcode.com/topic/29161/share-my-solutions-and-detailed-explanation-with-recursive-iterative-in-order-traversal-and-morris-traversal)
> 3.  [Morris Traversal方法遍历二叉树（非递归，不用栈，O(1)空间）](http://www.cnblogs.com/AnnieKim/archive/2013/06/15/MorrisTraversal.html)