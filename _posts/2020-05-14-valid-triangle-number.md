---
title: Implement Trie (Prefix Tree)
author: Soubhik Rakshit
date: 2020-05-14 20:30:00 -0400
categories: [Leetcode, Code]
tags: [medium, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/valid-triangle-number/){:target="_blank"}

**Problem Statement**

> Given an array consists of non-negative integers, your task is to count the number of triplets chosen from the array that can make triangles if we take them as side lengths of a triangle.

NOTE:
1. The length of the given array won't exceed 1000.
2. The integers in the given array are in the range of [0, 1000].

**Solution Approach**

* We sort the array and fix the first pointer index at the extreme end. We fix two other pointers, one at the beginning (pointing to the smallest element) and another pointing to just before the first pointer.
* If the sum of elements pointed to by `low` and `high` pointer is greater than the first pointer, that means all elements in the middle will create valid triangles. Thus, we add the difference between the indices of `high` and `low` pointer. Next, we decrement the `high` pointer.
* If not, then we increment the lower pointer and check whether the above condition is satisfied.
* This runs until all triplets are covered.

**Complexity**

* Time complexity - _O(n^2)_. This is almost like [**3sum**](posts/three-sum/).
* Space complexity - _O(1)_. Remember that `std::sort` is an in-place sorting algorithm.

```c++
class Solution {
public:
    int triangleNumber(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int count=0;
        for(int i=nums.size()-1; i>1; i--) {
            int low=0, high=i-1;
            
            while(low<high) {
                if(nums[low]+nums[high]>nums[i]) {
                    count+=high-low;
                    high--;
                }
                else
                    low++;
            }
        }
        return count;
    }
};
```