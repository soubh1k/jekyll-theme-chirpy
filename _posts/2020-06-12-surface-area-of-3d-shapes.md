---
title: Surface Area of 3D Shapes
author: Soubhik Rakshit
date: 2020-06-12 14:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/surface-area-of-3d-shapes/){:target="_blank"}

**Problem Statement**

> On a `N * N` grid, we place some `1 * 1 * 1` cubes.

> Each value `v = grid[i][j]` represents a tower of `v` cubes placed on top of grid cell `(i, j)`.

> Return the total surface area of the resulting shapes.

**Solution Approach**

* The total surface area is the following.
* **Surface area** = Surface area of all individual blocks - (surfaces which are common to the neighbors + surfaces which are in the middle of each stack of blocks).
* Surface area of all individual blocks =  6 * number of blocks.
* Surfaces which are common to the neighbors = Minimum of blocks in current cell to that of neighboring cell.
* Surfaces which are in the middle of each stack of blocks = 2 * (number of blocks in each stack - 1). However, this value cannot be negative.

**Complexity**

Let n be the size of grid.
* Time complexity - _O(n^2)_ traversing all cells.
* Space complexity - _O(1)_ as we don't need any extra space.

**Code**

```c++
class Solution {
public:
    int common(vector<vector<int>>& grid, int i, int j) {
        int common = 0;
        if(i>0)
            common += min(grid[i][j], grid[i-1][j]);
        if(i<grid.size()-1)
            common += min(grid[i][j], grid[i+1][j]);
        if(j>0)
            common += min(grid[i][j], grid[i][j-1]);
        if(j<grid[0].size()-1)
            common += min(grid[i][j], grid[i][j+1]);
            
        return common + max(0, 2*(grid[i][j]-1));
    }
    
    int surfaceArea(vector<vector<int>>& grid) {
        int total = 0;
        for(auto row:grid) {
            for(int num:row) {
                total += num;
            }
        }
        
        total = total * 6;
        
        for(int i=0; i<grid.size(); i++) {
            for(int j=0; j<grid[0].size(); j++) {
                total -= common(grid, i, j);
            }
        }
        
        return total;
    }
};
```