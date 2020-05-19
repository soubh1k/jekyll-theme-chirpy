---
title: Binary Search Tree to Greater Sum Tree
author: Soubhik Rakshit
date: 2020-05-18 23:30:00 -0400
categories: [Leetcode, Code]
tags: [medium, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/){:target="_blank"}

**Problem Statement**

> Given the root of a binary search tree with distinct values, modify it so that every `node` has a new value equal to the sum of the values of the original tree that are greater than or equal to `node.val`.
> As a reminder, a _binary search tree_ is a tree that satisfies these constraints:
> * The left subtree of a node contains only nodes with keys **less than** the node's key.
> * The right subtree of a node contains only nodes with keys **greater than** the node's key.
> * Both the left and right subtrees must also be binary search trees. 

CONSTRAINTS:

1. The number of nodes in the tree is between `1` and `100`.
2. Each node will have value between `0` and `100`.
3. The given tree is a binary search tree.

**Solution Approach**

* We shall visit the nodes in a reversed inorder approach. We keep a pointer which stores the running value of all nodes.
* On reaching a node, we increment the its value by the running value and set the value of the pointer to the value of the current node.

**Complexity**

Let `n` be the number of nodes and `h` be the height of the tree.
* Time complexity - _O(n)_, as we need to traverse `n` nodes once.
* Space complexity - _O(1)_, as we don't require any extra space. However, we have implicitly allocated _O(h)_ space in the stack for storing recursive calls.

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
    void modify(TreeNode* root, int *val) {
        if(root==NULL)
            return;
        modify(root->right, val);
        
        root->val += *val;
        *val = root->val;
        
        modify(root->left, val);
    }
    
    TreeNode* bstToGst(TreeNode* root) {
        int val=0;
        modify(root, &val);
        return root;
    }
};
```