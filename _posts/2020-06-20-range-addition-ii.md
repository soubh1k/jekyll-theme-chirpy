---
title: Range Addition II
author: Soubhik Rakshit
date: 2020-06-20 10:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/range-addition-ii/){:target="_blank"}

**Problem Statement**

> Given an m * n matrix **M** initialized with all **0**'s and several update operations.

> Operations are represented by a 2D array, and each operation is represented by an array with two **positive** integers **a** and **b**, which means **M[i][j]** should be **added by one** for all **0 <= i < a** and **0 <= j < b**.

> You need to count and return the number of maximum integers in the matrix after performing all the operations.

**Solution Approach**

* We need to return the intersection of all rectangles in the operations.
* Thus, the result will be the minimum x coordinate multiplied by the y coordinate.

**Complexity**

Let n be the number of operations.
* Time complexity - _O(n)_ to traverse all the operations.
* Space complexity - _O(1)_ as we don't use any extra space.

**Code**

```c++
class Solution {
public:
    int maxCount(int m, int n, vector<vector<int>>& ops) {
        if(ops.empty())
            return m*n;
        int minx = INT_MAX, miny = INT_MAX;
        
        for(auto& op : ops) {
            minx = min(minx, op[0]);
            miny = min(miny, op[1]);
        }
        
        return minx * miny;
    }
};
```