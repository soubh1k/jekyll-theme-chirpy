---
title: Check If All 1's Are at Least Length K Places Away
author: Soubhik Rakshit
date: 2020-06-02 10:10:00 -0400
categories: [Leetcode, Code]
tags: [medium, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/check-if-all-1s-are-at-least-length-k-places-away/){:target="_blank"}

**Problem Statement**

> Given an array `nums`  of 0s and 1s and an integer `k`, return `True` if all 1's are at least `k` places away from each other, otherwise return `False`.

CONSTRAINTS:

1. `1 <= nums.length <= 10^5`
2. `0 <= k <= nums.length`
3. `nums[i] is 0 or 1`

**Solution Approach**

* First, we find out the first `1` in the array. Next we calculate the distance between every successive pair of `1`s.
* If all distances are atleast `k` away from the first, we return `True`. Otherwise return `False`.

**Complexity**

* Time complexity - _O(n)_ to traverse all the input array elements.
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
    bool kLengthApart(vector<int>& nums, int k) {
        int last=0;
        while(last<nums.size() && nums[last]!=1)
            last++;

        for(int i=last+1; i<nums.size(); i++) {
            if(nums[i]==1) {
                if(i-last >= k+1)
                    last = i;
                else
                    return false;
            }
        }
        return true;
    }
};
```