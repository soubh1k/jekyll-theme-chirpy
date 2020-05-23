---
title: Interval List Intersections
author: Soubhik Rakshit
date: 2020-05-22 14:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, vector]
---

[**LeetCode Question Link**](https://leetcode.com/problems/interval-list-intersections/){:target="_blank"}

**Problem Statement**

> Given two lists of **closed** intervals, each list of intervals is pairwise disjoint and in sorted order.

> Return the intersection of these two interval lists.

> _(Formally, a closed interval `[a, b]` (with `a <= b`) denotes the set of real numbers `x` with `a <= x <= b`.  The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval.  For example, the intersection of [1, 3] and [2, 4] is [2, 3].)_

NOTE:

1. `0 <= A.length < 1000`
2. `0 <= B.length < 1000`
3. `0 <= A[i].start, A[i].end, B[i].start, B[i].end < 10^9`

**Solution Approach**

* Compare the first interval of A and B and find its common interval. It A ends before B increment A's pointer, else increment B's pointer and compare again.
* Repeat above step until any pointer reaches the end.

**Complexity**

Let m be the number of intervals in `A` and n be the number of intervals in `B`.
* Time complexity - _O(m+n)_. 
* Space complexity - _O(max(m, n))_ as there can be atmost _max(m, n)_ intervals in `result`.

**Code**

```c++
class Solution {
public:
    void common(vector<int> &A, vector<int> &B, vector<vector<int> > &result) {
        int low = max(A[0], B[0]);
        int high = min(A[1], B[1]);
        if(low <= high)
            result.push_back({low, high});
    }
    vector<vector<int>> intervalIntersection(vector<vector<int>>& A, vector<vector<int>>& B) {
        int i=0, j=0;
        
        vector<vector<int> > result;
        
        while(i<A.size() && j<B.size()) {
            common(A[i], B[j], result);
            if(A[i][1]<B[j][1])
                i++;
            else
                j++;
        }
        
        return result;
    }
};
```