---
title: Binary Tree Tilt
author: Soubhik Rakshit
date: 2020-05-17 16:30:00 -0400
categories: [Leetcode, Code]
tags: [easy, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/binary-tree-tilt/){:target="_blank"}

**Problem Statement**

> Given a binary tree, return the tilt of the **whole tree**.
> The tilt of a **tree node** is defined as the **absolute difference** between the sum of all left subtree node values and the sum of all right subtree node values. Null node has tilt 0.
> The tilt of the **whole tree** is defined as the sum of all nodes' tilt.

NOTE:

1. The sum of node values in any subtree won't exceed the range of 32-bit integer.
2. All the tilt values won't exceed the range of 32-bit integer.


**Solution Approach**

* We calculate the absolute difference between left and right subtree sum at every node and set it to `val`.
* Next, we just return the sum of the every value in the tree.

**Complexity**

Let n be the number of nodes in the tree.
* Time complexity - _O(n^2)_, as we have to traverse all the nodes in the tree for every node we want to find the sum.
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
    int findSum(TreeNode* root) {
        if(root==NULL)
            return 0;
        return root->val + findSum(root->left) + findSum(root->right);
    }
    
    void tilt(TreeNode* root) {
        if(root==NULL)
            return;
        
        root->val = abs(findSum(root->left) - findSum(root->right));
        
        if(root->left)
            findTilt(root->left);
        
        if(root->right)
            findTilt(root->right);
    }
    
    int findTilt(TreeNode* root) {
        if(root==NULL)
            return 0;
        tilt(root);
        return findSum(root);
    }
};
```