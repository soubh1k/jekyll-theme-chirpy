---
title: Add One Row to Tree
author: Soubhik Rakshit
date: 2020-05-24 21:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/add-one-row-to-tree/){:target="_blank"}

**Problem Statement**

> Given the root of a binary tree, then value `v` and depth `d`, you need to add a row of nodes with value `v` at the given depth `d`. The root node is at depth 1.

> The adding rule is: given a positive integer depth `d`, for each NOT null tree nodes `N` in depth `d-1`, create two tree nodes with value `v` as `N's` left subtree root and right subtree root. And `N's` **original left subtree** should be the left subtree of the new left subtree root, its **original right subtree** should be the right subtree of the new right subtree root. If depth `d` is 1 that means there is no depth d-1 at all, then create a tree node with value **v** as the new root of the whole original tree, and the original tree is the new root's left subtree.

NOTE:

1. The given d is in range [1, maximum depth of the given tree + 1].
2. The given binary tree has at least one tree node.

**Solution Approach**

* If d is 1, we create a node and set its left child equal to the root.
* Else we perform BFS, until we reach a node at height equal to d. Then we insert a new node in between its left and right children.

**Complexity**

Let n be the number of stones and V be the total sum of weights of all stones.
* Time complexity - _O(n)_ as all nodes need to be considered.
* Space complexity - _O(n)_ as the function call stack can have atmost n elements.

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
    void insert(TreeNode* root, int v, int d) {
        if(root==NULL)
            return;
        if(d==1) {
            TreeNode* newNode1 = new TreeNode(v);
            newNode1->left = root->left;
            root->left = newNode1;
            
            TreeNode* newNode2 = new TreeNode(v);
            newNode2->right = root->right;
            root->right = newNode2;
        }
        else {        
            insert(root->left, v, d-1);
            insert(root->right, v, d-1);
        }
    }
    
    TreeNode* addOneRow(TreeNode* root, int v, int d) {
        if(d==1) {
            TreeNode* newNode = new TreeNode(v);
            newNode->left = root;
            return newNode;
        }
        
        insert(root, v, d-1);
        return root;
    }
};
```