---
title: Binary Tree Pruning
author: Soubhik Rakshit
date: 2020-05-17 16:35:00 -0400
categories: [Leetcode, Code]
tags: [medium, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/binary-tree-pruning/){:target="_blank"}

**Problem Statement**

> We are given the head node `root` of a binary tree, where additionally every node's value is either a 0 or a 1.

> Return the same tree where every subtree (of the given tree) not containing a 1 has been removed.

> (Recall that the subtree of a node X is X, plus every node that is a descendant of X.)

NOTE:

1. The binary tree will have at most `100 nodes`.
2. The value of each node will only be `0`or `1`.

**Solution Approach**

* We calculate the whether each subtree contains `1`. If it doesn't then we make that subtree `NULL`.
* Otherwise, we keep pruning the left and right subtree.

**Complexity**

Let n be the number of nodes in the tree.
* Time complexity - _O(n^2)_, as we have to traverse all the nodes in the tree to check if 1 is present for every node in the tree.
* Space complexity - _O(1)_, as we don't use any memory explicitly. However, the stack trace will be of size _O(n)_ to store all function calls.

**Code**

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool containsOne(TreeNode* root) {
        if(root==NULL)
            return false;
        if(root->val==1)
            return true;
        return containsOne(root->left) || containsOne(root->right);
    }
    TreeNode* pruneTree(TreeNode* root) {
        if(root==NULL)
            return root;
        
        if(!containsOne(root->left))
            root->left = NULL;
        else
            root->left = pruneTree(root->left);
        
        if(!containsOne(root->right))
            root->right = NULL;
        else
            root->right = pruneTree(root->right);
        
        if(!root->left && !root->right && root->val==0)
            return NULL;
        
        return root;
    }
};
```