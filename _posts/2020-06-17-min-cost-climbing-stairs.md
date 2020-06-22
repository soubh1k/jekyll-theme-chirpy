---
title: Min Cost Climbing Stairs
author: Soubhik Rakshit
date: 2020-06-17 16:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, dp]
---

[**LeetCode Question Link**](https://leetcode.com/problems/min-cost-climbing-stairs/){:target="_blank"}

**Problem Statement**

> On a staircase, the `i`-th step has some non-negative cost `cost[i]` assigned (0 indexed).

> Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.

**Solution Approach**

* At every step, we find the minimum cost to reach that staircase. 
* Minimum cost is the cost of stepping in the staircase and the minimum cost of reaching the staircase from any of the two previous steps.

**Complexity**

* Time complexity - _O(n)_ to traverse all the elements in the array.
* Space complexity - _O(n)_ to store the minimum cost at each step in the stair case.

**Code**

```c++
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) {
        cost.push_back(0);
        vector<int> dp(cost.size());
        dp[0] = cost[0];
        dp[1] = cost[1];
        
        for(int i=2; i<dp.size(); i++) {
            dp[i] = min(dp[i-2], dp[i-1]) + cost[i];
        }
        
        return min(dp[dp.size()-1], dp[dp.size()-2]);
    }
};
```