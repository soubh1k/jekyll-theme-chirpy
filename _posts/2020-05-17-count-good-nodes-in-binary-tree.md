---
title: Count Good Nodes in Binary Tree
author: Soubhik Rakshit
date: 2020-05-17 12:30:00 -0400
categories: [Leetcode, Code]
tags: [medium, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/count-good-nodes-in-binary-tree/){:target="_blank"}

**Problem Statement**

> Given a binary tree `root`, a node _X_ in the tree is named **good** if in the path from root to _X_ there are no nodes with a value _greater than_ X.

> Return the number of **good** nodes in the binary tree.

**Solution Approach**

* We create boiler plate function to count the number of good nodes by passing a maximum value of all nodes from the `root` to the current node.
* Check if the current node is good. If it is we return the sum of good nodes in the left subtree, good nodes in right subtree and 1 if current node is good.

**Complexity**

Let n be the number of nodes in the tree.
* Time complexity - _O(n)_, as we have to traverse all the nodes in the tree.
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
    int countGood(TreeNode* root, int val) {
        if(root==NULL)
            return 0;
        int count=0;
        if(root->val >= val)
            count++;
        
        return count + countGood(root->left, max(val, root->val)) + countGood(root->right, max(val, root->val));
    }
    
    int goodNodes(TreeNode* root) {
        if(root==NULL)
            return 0;
        return countGood(root, root->val);
    }
};
```