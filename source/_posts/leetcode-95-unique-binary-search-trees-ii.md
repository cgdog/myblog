---
title: leetcode 95. Unique Binary Search Trees II
id: 790
categories:
  - algorithm
date: 2017-01-09 11:27:25
tags:
  - C++
  - Dynamic programming
  - leetcode
---

[95&#46; Unique Binary Search Trees II](https://leetcode.com/problems/unique-binary-search-trees-ii/)

Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1...n.

For example, Given n = 3, your program should return all 5 unique BST's shown below.
```
       1         3     3      2      1
        \       /     /      / \      \
         3     2     1      1   3      2
        /     /       \                 \
       2     1         2                 3
```

    DP solution:


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
        TreeNode* clone(TreeNode* root) {
            if (!root)
                return NULL;
            TreeNode* newroot = new TreeNode(root->val);
            newroot->left = clone(root->left);
            newroot->right = clone(root->right);
            return newroot;
        }
        vector<TreeNode*> generateTrees(int n) {
            if (n == 0) return vector<TreeNode*>();
            vector<TreeNode*> res(1, nullptr);
            for (int i = 1; i <= n; i++) {
                vector<TreeNode*> tmp;
                for (int j = 0; j < res.size(); j++) {
                    TreeNode* oldroot = res[j];
                    TreeNode* root = new TreeNode(i);
                    TreeNode* tree_copy = clone(oldroot);
                    root->left = tree_copy;
                    tmp.push_back(root);

                    if (oldroot) {
                        TreeNode* tmpold = oldroot;
                        while (tmpold->right) {
                            TreeNode* node = new TreeNode(i);
                            TreeNode* tmpright = tmpold->right;
                            tmpold->right = node;
                            tmpold->right->left = tmpright;
                            TreeNode* newtree = clone(oldroot);
                            tmp.push_back(newtree);
                            tmpold->right = tmpright;
                            tmpold = tmpold->right;
                        }
                        tmpold->right = new TreeNode(i);
                        TreeNode* newtree = clone(oldroot);
                        tmp.push_back(newtree);
                        tmpold->right = nullptr;
                    }
                }
                res = tmp;
            }
            return res;
        }
    };
```

    [https://discuss.leetcode.com/topic/6711/share-a-c-dp-solution-with-o-1-space](https://discuss.leetcode.com/topic/6711/share-a-c-dp-solution-with-o-1-space)

    ### recursive solution

``` cpp
/* Definition for a binary tree node. * struct TreeNode { * int val; * TreeNode *left; * TreeNode *right; * TreeNode(int x) : val(x), left(NULL), right(NULL) {} * }; */ 
    class Solution { public:

        vector<TreeNode*> genTrees(int start, int end) {
            vector<TreeNode*> res;
            if (start > end) {
                res.push_back(NULL);
                return res;
            }

            for (int idx = start; idx <= end; idx++) {
                vector<TreeNode*> lefttree = genTrees(start, idx-1);
                vector<TreeNode*> righttree = genTrees(idx+1, end);
                for (TreeNode* left : lefttree) {
                    for (TreeNode* right : righttree) {
                        TreeNode* root = new TreeNode(idx);
                        root->left = left;
                        root->right = right;
                        res.push_back(root);
                    }
                }
            }
            return res;
        }
        vector<TreeNode*> generateTrees(int n) {
            if (n == 0)
                return vector<TreeNode*>();
            return genTrees(1, n);
        }

    };
```
[https://discuss.leetcode.com/topic/3079/a-simple-recursive-solution](https://discuss.leetcode.com/topic/3079/a-simple-recursive-solution)