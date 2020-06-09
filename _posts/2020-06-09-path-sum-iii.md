---
title: Path Sum III
author: Soubhik Rakshit
date: 2020-06-09 12:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/path-sum-iii/){:target="_blank"}

**Problem Statement**

> You are given a binary tree in which each node contains an integer value.

> Find the number of paths that sum to a given value.

> The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

> The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

**Solution Approach**

* We start DFS from each and every node in the tree. So, its a recursion within a recursion.
* From a node, we start going through the left and right subtrees. If we find a path thats sums up to the target value, we increase the counter.

**Complexity**

Let n be the number of nodes in the tree.
* Time complexity - _O(n^2)_, since we run DFS from each node in the tree.
* Space complexity - _O(1)_, since, we don't require any space explicitly. However, the function call stack requires _O(n)_ space in the worst case.

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
    
    void paths(TreeNode* root, int val, int* count) {
        if(root==NULL)
            return;
        if(root->val == val)
            *count = *count + 1;

        paths(root->left, val-root->val, count);
        paths(root->right, val-root->val, count);
    }
    
    void findPaths(TreeNode* root, int sum, int* count) {
        if(root==NULL)
            return;

        findPaths(root->left, sum, count);

        if(root->val == sum)
            *count = *count + 1;
        paths(root->left, sum-root->val, count);
        paths(root->right, sum-root->val, count);
        findPaths(root->right, sum, count);
    }
    
    int pathSum(TreeNode* root, int sum) {
        int count = 0;
        findPaths(root, sum, &count);
        return count;
    }
};
```