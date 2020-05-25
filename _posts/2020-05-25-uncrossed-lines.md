---
title: Uncrossed Lines
author: Soubhik Rakshit
date: 2020-05-25 11:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, dp]
---

[**LeetCode Question Link**](https://leetcode.com/problems/uncrossed-lines/){:target="_blank"}

**Problem Statement**

> We write the integers of A and B (in the order they are given) on two separate horizontal lines.

> Now, we may draw connecting lines: a straight line connecting two numbers A[i] and B[j] such that:

> * A[i] == B[j];
> * The line we draw does not intersect any other connecting (non-horizontal) line.

> Note that a connecting lines cannot intersect even at the endpoints: each number can only belong to one connecting line.

> Return the maximum number of connecting lines we can draw in this way.

NOTE:

1. `1 <= A.length <= 500`
2. `1 <= B.length <= 500`
3. `1 <= A[i], B[i] <= 2000`

**Solution Approach**

* This problem is exactly similar to that of finding the longest common subsequence.
* We create a memoization table `dp` where `dp[i][j]` is the maximum uncrossed lines that can be drawn using A[0...i] and B[0...j].
* At every step, we have 2 choices: either include or exclude the current pair. If we include the current pair, then `dp[i][j] = dp[i-1][j-1] + 1`, else `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`.
* The result is the last element in the table.


**Complexity**

Let m and n be the size of A and B respectively.
* Time complexity - _O(mn)_ as all nodes need to be considered.
* Space complexity - _O(mn)_ as the function call stack can have atmost n elements.

**Code**

```c++
// #define max(x,y) (x>y?x:y)
class Solution {
public:
    int maxUncrossedLines(vector<int>& A, vector<int>& B) {
        vector<vector<int> > dp(A.size()+1, vector<int> (B.size()+1, 0));
        
        for(int i=1; i<dp.size(); i++) {
            for(int j=1; j<dp[0].size(); j++) {
                if(A[i-1] == B[j-1])
                    dp[i][j] = dp[i-1][j-1] + 1;
                else
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
        
        return dp.back().back();
        
    }
};
```