---
title: Minimum Distance Between BST Nodes
author: Soubhik Rakshit
date: 2020-06-10 14:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/minimum-distance-between-bst-nodes/){:target="_blank"}

**Problem Statement**

> Given a Binary Search Tree (BST) with the root node `root`, return the minimum difference between the values of any two different nodes in the tree.

NOTE:

1. The size of the BST will be between `2` and `100`.
2. The BST is always valid, each node's value is an integer, and each node's value is different.
3. This question is the same as 530: https://leetcode.com/problems/minimum-absolute-difference-in-bst/

**Solution Approach**

* Inorder traversal returns sorted order of elements in a BST. So, perform inorder traversal and compare each element with the last element found.

**Complexity**

* Time complexity - _O(n)_ traversing the entire tree.
* Space complexity - _O(1)_ as we don't need any extra space.

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
    
    void find_diff(TreeNode* root, int *last, int* min_diff, bool* first) {
        if(root==NULL)
            return;
        
        find_diff(root->left, last, min_diff, first);
        
        if(*first) {
            *last = root->val;
            *first = false;
        }
        else {
            *min_diff = min(*min_diff, root->val - *last);
            *last = root->val;
        }
        
        find_diff(root->right, last, min_diff, first);
    }
    
    int minDiffInBST(TreeNode* root) {
        int last = 0;
        int min_diff = INT_MAX;
        bool first = true;
        find_diff(root, &last, &min_diff, &first);
        return min_diff;
    }
};
```