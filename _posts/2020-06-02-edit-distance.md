---
title: Delete Node in a Linked List
author: Soubhik Rakshit
date: 2020-06-02 10:25:00 -0400
categories: [Leetcode, Code]
tags: [hard, dp]
---

[**LeetCode Question Link**](https://leetcode.com/problems/edit-distance/){:target="_blank"}

**Problem Statement**

> Given two words word1 and word2, find the minimum number of operations required to convert word1 to word2.
> You have the following 3 operations permitted on a word:

> 1. Insert a character
> 2. Delete a character
> 3. Replace a character

**Solution Approach**

Let input word sizes be `m` and `n`.
* Create table `dp` of size `m+1` by `n+1` where `dp[i][j]` is the the edit distance between word1[0...i] and word2[0...j].
* Initialize table by setting the first row and first column as `0,1,...,m` and `0,1,...,n` respectively. This means if either of those strings are empty, then the edit distance would be the length of the other string.
* Iterate through all cells in the table in row wise manner.
* If `i`th character in `word1` is equal to `j`th character in `word2`, then set value of the table as the value in `i-1`th row and `j-1`th column in the table. This is because if the two characters being compared is the same, then it does not contribute to the edit distance.
* If those two characters are not the same, then set the value of the cell as the minimum of the values of cells towards its immediate left, immediate top and immediate top left cell. Add 1 to this value. This is because if the two characters being compared are not the same, then the edit distance between `word1[0...i]` and `word2[0...j]` is equal to the minimum value of those 3 cells + 1.
* The result is the last element in the table.

**Complexity**

Let size of input strings be `m` and `n`,
* Time complexity - _O(mn)_, since we use only 2 constant time operations.
* Space complexity - _O(mn)_, since we don't need any extra space.

**Code**

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word1.size()+1, vector<int> (word2.size()+1));
        for(int i=0; i<word1.size()+1; i++)
            dp[i][0] = i;
        for(int j=0; j<word2.size()+1; j++)
            dp[0][j] = j;
        
        
        for(int i=1; i<word1.size()+1; i++) {
            for(int j=1; j<word2.size()+1; j++) {
                if(word1[i-1]==word2[j-1])
                    dp[i][j] = dp[i-1][j-1];
                else {
                    dp[i][j] = min(dp[i-1][j-1], min(dp[i][j-1], dp[i-1][j]))+1;
                }
            }
        }
        
        return dp.back().back();
    }
};
```

**Final Thoughts**

This problem can be solved in O(min(m,n)) space as we only need to store the values in the last row instead of the entire table.