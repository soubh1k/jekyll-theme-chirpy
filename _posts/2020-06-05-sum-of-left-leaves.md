---
title: Sum of Left Leaves
author: Soubhik Rakshit
date: 2020-06-05 17:10:00 -0400
categories: [Leetcode, Code]
tags: [easy, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/sum-of-left-leaves/){:target="_blank"}

**Problem Statement**

> Find the sum of all left leaves in a given binary tree.

**Solution Approach**

* For every node that has both left and right children and left child is not a leaf, the result is sum of left leaves in left and right subtrees.
* If the left child is a leaf, then result is sum of value of left node and left leaves in right subtree.

**Complexity**

Let n be the number of nodes in the tree.
* Time complexity - _O(n)_, since we traverse through all nodes.
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
    int sumOfLeftLeaves(TreeNode* root) {
        if(root==NULL) return 0;
        
        int left = sumOfLeftLeaves(root->left);
        int right = sumOfLeftLeaves(root->right);
        
        if(root->left && !root->left->left && !root->left->right)
            return root->left->val + right;
        else
            return left + right;
    }
};
```