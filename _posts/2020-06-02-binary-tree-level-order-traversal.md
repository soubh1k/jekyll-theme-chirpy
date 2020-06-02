---
title: Binary Tree Level Order Traversal
author: Soubhik Rakshit
date: 2020-06-02 10:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, tree]
---

[**LeetCode Question Link**](https://leetcode.com/problems/binary-tree-level-order-traversal/){:target="_blank"}

**Problem Statement**

> Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

**Solution Approach**

* We use 2 queues. `q` stores the nodes at the current level and `temp_level` store the nodes at the next level. After we finish processing all nodes in `q`, we set `q = temp_level`.
* We repeat this process until there are no more nodes in the next level.

**Complexity**

* Time complexity - _O(n)_ to traverse all the nodes in the tree once.
* Space complexity - _O(2n)_, since we need to store the entire return array in the queue at worst case.

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int> > result;
        if(root==NULL)
            return result;
        queue<TreeNode*> q;
        q.push(root);
        
        while(!q.empty()) {
            vector<int> level;
            queue<TreeNode*> temp_level;
            while(!q.empty()) {
                TreeNode* temp = q.front();
                q.pop();
                level.push_back(temp->val);
                if(temp->left)
                    temp_level.push(temp->left);
                if(temp->right)
                    temp_level.push(temp->right);
            }
            q = temp_level;
            result.push_back(level);
        }
        
        return result;
    }
};
```