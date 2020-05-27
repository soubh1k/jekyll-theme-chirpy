---
title: Diameter of Binary Tree
author: Soubhik Rakshit
date: 2020-05-26 22:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/diameter-of-binary-tree/){:target="_blank"}

**Problem Statement**

> Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the **longest** path between any two nodes in a tree. This path may or may not pass through the root.

NOTE:

The length of path between two nodes is represented by the number of edges between them.

**Solution Approach**

* If a particular node is the root of the solution, then the maximum length of longest path is the sum of height of left and right subtree of the node. Otherwise, we pass the maximum height of left and right to the parent nodes.

**Complexity**

Let n be the number of nodes
* Time complexity - _O(n)_ to traverse all the nodes.
* Space complexity - _O(1)_. However, nodes are stored in the stack during recursion and it may have worst space complexity of _O(n)_.

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
    int findDiameter(TreeNode* root, int* result) {
        if(root==NULL)
            return 0;
        int left = findDiameter(root->left, result);
        int right = findDiameter(root->right, result);
        
        *result = max(*result, left+right+1);
        return max(left+1, right+1);
    }
    
    int diameterOfBinaryTree(TreeNode* root) {
        if(root==NULL)
            return 0;
        int result = 0;
        findDiameter(root, &result);
        return result-1;
    }
};
```