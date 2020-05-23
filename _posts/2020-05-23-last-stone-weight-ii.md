---
title: Last Stone Weight II
author: Soubhik Rakshit
date: 2020-05-23 12:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/last-stone-weight-ii/){:target="_blank"}

**Problem Statement**

> We have a collection of rocks, each rock has a positive integer weight.

> Each turn, we choose **any two rocks** and smash them together.  Suppose the stones have weights `x` and `y` with `x <= y`.  The result of this smash is:

> * If `x == y`, both stones are totally destroyed;

> * If `x != y`, the stone of weight `x` is totally destroyed, and the stone of weight `y` has new weight `y-x`.

> At the end, there is at most 1 stone left.  Return the **smallest possible** weight of this stone (the weight is 0 if there are no stones left.)

NOTE:

1. `1 <= stones.length <= 30`
2. `1 <= stones[i] <= 100`

**Solution Approach**

* This is a 0-1 knapsack problem where we have to select stones close to half of sum of weights of all stones in 1 knapsack and all the remaining stones in the other knaspsack.
* Next, the difference between the weights of both knapsacks is the answer.
* We use dynamic programming to solve knapsack problem.
* We use half of the total sum as the maximum weight of the smaller knapsack. Then, we perform 0-1 knapsack using all stones where value of each stone is equal to its weight.

**Complexity**

Let n be the number of stones and V be the total sum of weights of all stones.
* Time complexity - _O(nV)_. Note that this is pseudopolynomial as it depends on V which can get very large.
* Space complexity - _O(nV)_, to store the memoization table.

**Code**

```c++
class Solution {
public:
    int lastStoneWeightII(vector<int>& stones) {
        int sum = 0;
        for(int num:stones)
            sum += num;
        
        vector<vector<int> > dp(stones.size()+1, vector<int> (sum/2+1, 0));
        
        for(int i=1; i<dp.size(); i++) {
            for(int j=1; j<dp[0].size(); j++) {
                if(stones[i-1]<=j) {
                    dp[i][j] = max(dp[i-1][j], max(dp[i][j-1], dp[i-1][j-stones[i-1]]+stones[i-1]));
                }
                else
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
        
        int max_val = dp.back().back();
        int max_val2 = sum-max_val;
        
        return abs(max_val2 - max_val);
    }
};
```