---
title: Largest Divisible Subset
author: Soubhik Rakshit
date: 2020-06-14 12:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/largest-divisible-subset/){:target="_blank"}

**Problem Statement**

> Given a set of **distinct** positive integers, find the largest subset such that every pair (S<sub>i</sub>, S<sub>j</sub>) of elements in this subset satisfies:

> S<sub>i</sub> % S<sub>j</sub> = 0 or S<sub>j</sub> % S<sub>i</sub> = 0.

> If there are multiple solutions, return any subset is fine.

**Solution Approach**

* We sort the array so that all divisors of an element comes before that element in the array.
* We traverse the elements of the array and each item in _count_ stores the number of elements in a valid subset containing that element.

**Complexity**

Let n be the size of array.
* Time complexity - _O(n^2)_ traversing all previous items in array for every item in the array.
* Space complexity - _O(n)_ as we store the number of divisors as well as the previous element in the chain.

**Code**

```c++
class Solution {
public:
    vector<int> largestDivisibleSubset(vector<int>& nums) {
        vector<int> result;
        
        if(nums.size()==0)
            return result;
        
        sort(nums.begin(), nums.end());
        
        vector<int> count(nums.size(), 1);
        vector<int> prev(nums.size(), -1);
        
        int maxindex = 0;
        
        for(int i=1; i<nums.size(); i++) {
            for(int j=0; j<i; j++) {
                if(nums[i]%nums[j]==0) {
                    if(count[i]<=count[j]) {
                        count[i] = count[j]+1;
                        prev[i] = j;
                    }
                }
            }
            if(count[maxindex]<count[i])
                maxindex = i;
        }
        
        while(maxindex>=0) {
            result.push_back(nums[maxindex]);
            maxindex = prev[maxindex];
        }

        return result;
    }
};
```