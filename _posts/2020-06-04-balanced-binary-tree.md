---
title: Balanced Binary Tree
author: Soubhik Rakshit
date: 2020-06-04 21:50:00 -0400
categories: [Leetcode, Code]
tags: [easy, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/balanced-binary-tree/){:target="_blank"}

**Problem Statement**

> Given a binary tree, determine if it is height-balanced.

> For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

**Solution Approach**

* A top down approach would involve calculating left and right subtree depths at every node. This process would have a time complexity of _O(n^2)_.
* However, we have used a bottom up approach where we calculate the height of left and right subtree at the bottom of the tree and pass it upwards.

**Complexity**

* Time complexity - _O(n)_, since we use only 2 constant time operations.
* Space complexity - _O(1)_, since we don't need any extra space.

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
    int height(TreeNode* root) {
        if(root==NULL)
            return 0;
        
        int left = height(root->left);
        if(left == -1)
            return left;
        int right = height(root->right);
        if(right == -1)
            return right;
        
        if(abs(left-right)>1)
            return -1;
        return max(left, right)+1;
        
    }
    
    bool isBalanced(TreeNode* root) {
        if(height(root)==-1)
            return false;
        return true;            
    }
};
```