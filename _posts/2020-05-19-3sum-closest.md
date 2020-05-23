---
title: 3Sum Closest
author: Soubhik Rakshit
date: 2020-05-19 16:00:00 -0400
categories: [Leetcode, Code]
tags: [hard, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/3sum-closest/){:target="_blank"}

**Problem Statement**

> Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. 

> You may assume that each input would have exactly one solution.

**Solution Approach**

* We use the normal 3Sum solution. First we sort the array. Then use 3 pointers method.
* First fix pointer `i` to the 1st array element. Fix `j` to the second element and `k` to the last element.
* We find the difference w.r.t target at every step. We keep track of minimum difference and maintain the `bestSum`. 

**Complexity**

Let `n` be the size of the array.
* Time complexity - _O(n^2)_. We use _O(n log n)_ for sorting and _O(n^2)_ for traversing all triplets using 3 pointers.
* Space complexity - _O(1)_ as we don't use any extra space.

**Code**

```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(), nums.end());
        int diff = INT_MAX;
        int bestSum=0;
        for(int i=0; i<nums.size()-2; i++) {
            int j=i+1, k=nums.size()-1;
            while(j<k) {
                int val = nums[i]+nums[j]+nums[k];
                cout<<abs(target-val)<<" "<<diff<<endl;
                if(abs(target-val)<diff) {
                    diff = abs(target-val);
                    bestSum = val;
                }
                if(val==target) {
                    return target;
                }
                else if(val>target)
                    k--;
                else
                    j++;
            }
        }
        return bestSum;
    }
};
```