---
title: Search in a Binary Search Tree
author: Soubhik Rakshit
date: 2020-06-16 12:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/search-in-a-binary-search-tree/){:target="_blank"}

**Problem Statement**

> Given the root node of a binary search tree (BST) and a value. You need to find the node in the BST that the node's value equals the given value. Return the subtree rooted with that node. If such node doesn't exist, you should return NULL.

**Solution Approach**

* We use BST properties and search for a the node in only that subtree which could contain the node of the target value.

**Complexity**

Let n be the number of nodes in the tree.
* Time complexity - _O(n)_ in worst case if all nodes have only one child. If the tree is balanced then the time complexity would be _O(1)_.
* Space complexity - _O(n)_ in worst case to store the function calls.

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
    TreeNode* searchBST(TreeNode* root, int val) {
        if(root==NULL)
            return NULL;
        if(root->val==val)
            return root;
        if(val<root->val)
            return searchBST(root->left, val);
        else return searchBST(root->right, val);
    }
};
```