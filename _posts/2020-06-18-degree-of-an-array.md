---
title: Degree of an Array
author: Soubhik Rakshit
date: 2020-06-18 10:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/degree-of-an-array/){:target="_blank"}

**Problem Statement**

> Given a non-empty array of non-negative integers `nums`, the **degree** of this array is defined as the maximum frequency of any one of its elements.

Your task is to find the smallest possible length of a (contiguous) subarray of `nums`, that has the same degree as `nums`.

**Solution Approach**

* First, we find the set of most frequent elements.
* Then, for each most frequent element, we find the left and right occurence of that element.
* We return the smallest subarray that has the minimum difference between left and right.

**Complexity**

* Time complexity - _O(n^2)_ in worst case when frequency of every element is the same.
* Space complexity - _O(n)_ to store the most frequent elements.

**Code**

```c++
class Solution {
public:
    int findShortestSubArray(vector<int>& nums) {
        unordered_map<int, int> m;
        int maxCount = 0;
        vector<int> bestNums;
        
        for(int n:nums) {
            if(m.find(n)==m.end())
                m[n] = 1;
            else
                m[n]++;
            
            if(m[n]>maxCount) {
                maxCount = m[n];
                bestNums = {n};
            }
            else if(m[n]==maxCount) {
                bestNums.push_back(n);
            }
        }
        
        int minDist = INT_MAX;
        for(int bestNum : bestNums) {
            int i,j;
            for(i=0; i<nums.size(); i++) {
                if(nums[i]==bestNum)
                    break;
            }
            for(j=nums.size()-1; j>=0; j--) {
                if(nums[j]==bestNum)
                    break;
            }
            minDist = min(minDist, j-i+1);
        }
        return minDist;
    }
};
```