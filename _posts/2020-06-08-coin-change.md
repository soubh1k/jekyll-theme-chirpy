---
title: Coin Change
author: Soubhik Rakshit
date: 2020-06-08 11:50:00 -0400
categories: [Leetcode, Code]
tags: [medium, dp]
---

[**LeetCode Question Link**](https://leetcode.com/problems/coin-change/){:target="_blank"}

**Problem Statement**

> You are given coins of different denominations and a total amount of money _amount_. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return `-1`.

**Solution Approach**

* This problem can be solved by Dynamic Programming as it has both an optimal substructure as well as the recursive solution having overlapping subproblems.
* We show optimal substructure by showing that a bigger problem can be solved using multiple subproblems. Here 
_f(i) = min\_j={0,1,...,n-1} {f(i-c\_j) + 1}_, where c\_j are the coin denominations.
* At every cell, we try including and excluding every coin seen till now to get the required amount.
* We save the minimum number of coins required to get the amount as denoted by the column.

**Complexity**

Let n be the number of coins.
* Time complexity - _O(amount * n)_, since we fill up the cells in the memoization table each in constant time.
* Space complexity - _O(amount * n)_, since, we store the memoization table with these many cells. However, as we only require the last row for calculating the value at each cell, we can reduce space complexity to _O(amount)_.

**Code**

```c++
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<vector<int> > dp(coins.size(), vector<int> (amount+1, amount+1));
        for(int i=0; i<coins.size(); i++)
            dp[i][0] = 0;
        
        for(int i=0; i<coins.size(); i++) {
            for(int j=1; j<amount+1; j++) {
                for(int k=0; k<=i; k++) {
                    if(j-coins[k]>=0)
                        dp[i][j] = min(dp[i][j], dp[k][j-coins[k]] + 1);
                }
            }
        }
        return dp.back().back()<=amount?dp.back().back():-1;
    }
};
```

**Final Thoughts**

This problem can be solved in O(amount) space as we only need to store the values in the last row instead of the entire table.