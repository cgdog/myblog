---
title: leetCode Validate Binary Search Tree
tags:
  - BST
  - leetcode
id: 450
categories:
  - algorithm
date: 2016-09-26 15:42:55
---

[Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/)

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

> *   The left subtree of a node contains only nodes with keys less than the node's key.
> *   The right subtree of a node contains only nodes with keys greater than the node's key.
> *   Both the left and right subtrees must also be binary search trees.

**Example 1:**

<pre>
    2
   / \
  1   3
</pre>

Binary tree **[2,1,3]**, return true.

**Example 2:**

<pre>
    1
   / \
  2   3
</pre>

Binary tree **[1,2,3]**, return false.



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
    bool valid(TreeNode* node, TreeNode* &pre) {
        if (node == NULL) {
            return true;
        }
        if (!valid(node->left, pre)) return false;
        if (pre != NULL && pre->val >= node->val) return false;
        pre = node;
        return valid(node->right, pre);
    }
    bool isValidBST(TreeNode* root) {

        TreeNode* pre = NULL;
        return valid(root, pre);
    }
};
```

大概的思路：使用中序遍历，遍历一棵二叉查找树(binary search tree)，得到的是一个关键字递增(ascending)的列表。上述代码**valid(TreeNode* node, TreeNode* &amp;pre)**用引用类型的参数pre，保存中序遍历过程中上次遍历的结点(值应该比当前结点的值小)。

> Reference:[https://discuss.leetcode.com/topic/4659/c-in-order-traversal-and-please-do-not-rely-on-buggy-int_max-int_min-solutions-any-more](https://discuss.leetcode.com/topic/4659/c-in-order-traversal-and-please-do-not-rely-on-buggy-int_max-int_min-solutions-any-more)

二叉树(Binary tree)中序遍历(Inorder traversal)的三种写法:[http://blog.csdn.net/hevc_cjl/article/details/28681977](http://blog.csdn.net/hevc_cjl/article/details/28681977)

二叉树的遍历：[http://www.cnblogs.com/dolphin0520/archive/2011/08/25/2153720.html](http://www.cnblogs.com/dolphin0520/archive/2011/08/25/2153720.html)