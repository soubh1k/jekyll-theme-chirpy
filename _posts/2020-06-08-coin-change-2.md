---
title: Coin Change 2
author: Soubhik Rakshit
date: 2020-06-08 12:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, dp]
---

[**LeetCode Question Link**](https://leetcode.com/problems/coin-change-2/){:target="_blank"}

**Problem Statement**

> You are given coins of different denominations and a total amount of money. Write a function to compute the number of combinations that make up that amount. You may assume that you have infinite number of each kind of coin.

**Solution Approach**

* This problem is like [**Coin Change**]({{site.url}}/posts/coin-change/) except we need to find the number of ways we can reach the solution.
* This problem can be solved by dynamic programming as well. We fill a cell in the same memoization table as earlier by including and excluding the current coin.
* Without using any coin, we can never reach the target. So, we initialize the table with 0.
* However, without using any coin, we can reach a target amount of `0` in `1` way. So, the first item in the table is 1.
* If we exclude the current coin, then the number of ways to reach the target is same as the number of ways we found earlier for the current cell.
* However, if we include the current coin _i_, we need to know the number of ways to make up amount _j-coins[i-1]_ using first _i_ coins which is _dp[i][j-coins[i-1]]_.

**Complexity**

Let n be the number of coins.
* Time complexity - _O(amount * n)_, since we fill up the cells in the memoization table n times each in constant time.
* Space complexity - _O(amount)_, since, we store the memoization table with only 1 row.

**Code**

```c++
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        vector<int> dp(amount+1, 0);
        dp[0] = 1;
        
        for(int i=1; i<coins.size()+1; i++) {
            for(int j=1; j<amount+1; j++) {
                if(j-coins[i-1]>=0)
                    dp[j] += dp[j-coins[i-1]];
            }
        }
            
        return dp[amount];
    }
};
```