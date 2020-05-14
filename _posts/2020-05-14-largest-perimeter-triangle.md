---
title: Largest Perimeter Triangle
author: Soubhik Rakshit
date: 2020-05-14 19:10:00 -0400
categories: [Leetcode, code]
tags: [easy, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/largest-perimeter-triangle/){:target="_blank"}

**Problem Statement**

> Given an array `A` of positive lengths, return the largest perimeter of a triangle with **non-zero area**, formed from 3 of these lengths.
> If it is impossible to form any triangle of non-zero area, return `0`.

NOTE:
1. `3 <= A.length <= 10000`
2. `1 <= A[i] <= 10^6`

**Solution Approach**

* We start by sorting the array and check whether triangle inequality is satisfied by the last three elements.
* If it is satisfied, we have found the triangle with the largest possible perimeter.
* Otherwise, shift the elements to the left and check.
* If no non-zero sized triangles are found, we return `0`.


**Complexity**

Let _n_ be the size of the input array.
* Time complexity - _O(n log n))_, 
* Space complexity - _O(1)_, as we are not using any extra space. Also `std::sort` is an in-place sorting algorithm.

**Code**

```c++
class Solution {
public:
    int largestPerimeter(vector<int>& A) {
        sort(A.begin(), A.end());
        for(int i=A.size()-1; i>1; i--) {
            if(A[i]<A[i-1]+A[i-2])
                return A[i]+A[i-1]+A[i-2];
        }
        return 0;
    }
};
```