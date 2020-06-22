---
title: Surrounded Regions
author: Soubhik Rakshit
date: 2020-06-18 11:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, graph]
---

[**LeetCode Question Link**](https://leetcode.com/problems/surrounded-regions/){:target="_blank"}

**Problem Statement**

> Given a 2D board containing `'X'` and `'O'` (**the letter O**), capture all regions surrounded by `'X'`.

> A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region.

**Solution Approach**

* First, we change all `'O'`s in the border to `'-'`s.
* Next, we iterate through the matrix and perform DFS from every position which has `'-'` and change all reachable cells to a `'.'`.
* Next, we know that cells with `'O'` are originally unreachable. Thus those cells must be captured and they must be flipped to `'X'`.
* Also, all `'.'` are the cells which could not be captured. So we change them back to  `'O'`.

**Complexity**

Let m and n be the dimensions of the matrix.
* Time complexity - _O(mn)_ in worst case when frequency of every element is the same.
* Space complexity - _O(1)_ since all operations are in place. However, DFS might have a worst case time complexity of _O(mn)_ to store the function call stack.

**Code**

```c++
class Solution {
public:
    void fill(vector<vector<char>>& board, int i, int j) {
        board[i][j] = '.';
        if(i>0 && board[i-1][j]=='O')
            fill(board, i-1, j);
        if(i<board.size()-1 && board[i+1][j]=='O')
            fill(board, i+1, j);
        if(j>0 && board[i][j-1]=='O')
            fill(board, i, j-1);
        if(j<board[0].size()-1 && board[i][j+1]=='O')
            fill(board, i, j+1);
    }
    
    void solve(vector<vector<char>>& board) {
        if(board.size()==0 || board[0].size()==0)
            return;
        for(int i=0; i<board.size(); i++) {
            if(board[i][0]=='O')
                board[i][0] = '-';
            if(board[i][board[0].size()-1]=='O')
                board[i][board[0].size()-1] = '-';
        }
        for(int i=0; i<board[0].size(); i++) {
            if(board[0][i]=='O')
                board[0][i] = '-';
            if(board[board.size()-1][i]=='O')
                board[board.size()-1][i] = '-';
        }
        
        for(int i=0; i<board.size(); i++) {
            for(int j=0; j<board[0].size(); j++) {
                if(board[i][j]=='-') {
                    fill(board, i, j);
                }
            }
        }
        
        transform(board.begin(), board.end(), board.begin(), [](vector<char> row) {
            transform(row.begin(), row.end(), row.begin(), [](char ch) {
                if(ch=='O')
                    return 'X';
                else if(ch=='.')
                    return 'O';
                else return ch;
            });
            return row;
        });
    }
};
```