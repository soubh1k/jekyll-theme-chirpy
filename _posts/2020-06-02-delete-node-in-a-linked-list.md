---
title: Delete Node in a Linked List
author: Soubhik Rakshit
date: 2020-06-02 10:20:00 -0400
categories: [Leetcode, Code]
tags: [easy, linked list]
---

[**LeetCode Question Link**](https://leetcode.com/problems/delete-node-in-a-linked-list/){:target="_blank"}

**Problem Statement**

> Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

**Solution Approach**

* Set current node value equal to next node value.
* Skip next node by setting current next node pointer to next of next node pointer.

**Complexity**

* Time complexity - _O(1)_, since we use only 2 constant time operations.
* Space complexity - _O(1)_, since we don't need any extra space.
**Code**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    void deleteNode(ListNode* node) {
        node->val = node->next->val;
        node->next = node->next->next;
    }
};
```