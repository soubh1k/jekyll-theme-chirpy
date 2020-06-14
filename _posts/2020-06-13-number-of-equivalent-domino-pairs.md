---
title: Number of Equivalent Domino Pairs
author: Soubhik Rakshit
date: 2020-06-13 22:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string, hashing]
---

[**LeetCode Question Link**](https://leetcode.com/problems/number-of-equivalent-domino-pairs/){:target="_blank"}

**Problem Statement**

> Given a list of `dominoes`, `dominoes[i] = [a, b]` is _equivalent_ to `dominoes[j] = [c, d]` if and only if either `(a==c and b==d)`, or `(a==d and b==c)` - that is, one domino can be rotated to be equal to another domino.

> Return the number of pairs `(i, j)` for which `0 <= i < j < dominoes.length`, and `dominoes[i]` is equivalent to `dominoes[j]` .

**Solution Approach**

* We store the dominoes by as a hashmap with each pair as the key and its count as the value.
* We sort the pair by keeping the smaller item as the first value and the larger item as the second value.
* We traverse through all the keys and calculate the number of equivalent matches.

**Complexity**

Let n be the size of grid.
* Time complexity - _O(n^2)_ traversing all cells.
* Space complexity - _O(1)_ as we don't need any extra space.

**Code**

```c++
struct hash_pair {
   template <class T1, class T2>
   size_t operator()(const pair<T1, T2>& p) const{
      auto hash1 = hash<T1>{}(p.first);
      auto hash2 = hash<T2>{}(p.second);
      return hash1 ^ hash2;
   }
};

class Solution {
public:
    int nc2(int n) {
        return n*(n-1)/2;
    }
    
    int numEquivDominoPairs(vector<vector<int>>& dominoes) {
        unordered_map<pair<int, int>, int, hash_pair> doms;
        int count;
        for(int i=0; i<dominoes.size(); i++) {
            int a = min(dominoes[i][0], dominoes[i][1]);
            int b = max(dominoes[i][0], dominoes[i][1]);
            
            if(doms.find({a,b})!=doms.end())
                doms[{a,b}] += 1;
            else
                doms[{a,b}] = 1;
        }
        
        int result = 0;
        for(auto it = doms.begin(); it != doms.end(); it++) {
            result += nc2(it->second);
        }
        
        return result;
    }
};
```