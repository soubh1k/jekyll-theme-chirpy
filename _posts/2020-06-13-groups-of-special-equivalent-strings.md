---
title: Groups of Special Equivalent Strings
author: Soubhik Rakshit
date: 2020-06-13 20:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string, hashing]
---

[**LeetCode Question Link**](https://leetcode.com/problems/groups-of-special-equivalent-strings/){:target="_blank"}

**Problem Statement**

> You are given an array `A` of strings.

> A _move onto_ `S` consists of swapping any two even indexed characters of `S`, or any two odd indexed characters of `S`.

> Two strings `S` and `T` are _special-equivalent_ if after any number of moves onto `S`, `S == T`.

> For example, `S = "zzxy"` and `T = "xyzz"` are special-equivalent because we may make the moves `"zzxy" -> "xzzy" -> "xyzz"` that swap `S[0]` and `S[2]`, then `S[1]` and `S[3]`.

> Now, a _group of special-equivalent strings_ from `A` is a non-empty subset of `A` such that:

1. Every pair of strings in the group are special equivalent, and;
2. The group is the largest size possible (ie., there isn't a string S not in the group such that S is special equivalent to every string in the group)

> Return the number of groups of special-equivalent strings from `A`.

**Solution Approach**

* We create a unique fingerprint for each set of equivalent strings by separately sorting the odd and even positions in the string and concatenating them.
* We store this unique fingerprints in an unordered set of strings.
* Finally, return the number of strings.

**Complexity**

Let n be the number of strings and s be the maximum size of a string.
* Time complexity - _O(n*s)_ to create the fingerprint of each string.
* Space complexity - _O(n*s)_ to store the fingerprint of each string.

**Code**

```c++
class Solution {
public:
    string arrange(string str) {
        string odd = "";
        string even = "";
        
        for(int i=0; i<str.size(); i+=2) {
            odd += str[i];
        }
        
        for(int i=1; i<str.size(); i+=2) {
            even += str[i];
        }
        
        sort(odd.begin(), odd.end());
        sort(even.begin(), even.end());
        
        return odd+even;
    }
    
    int numSpecialEquivGroups(vector<string>& A) {
        unordered_set<string> s;
        
        for(int i=0; i<A.size(); i++) {
            string temp = arrange(A[i]);
            if(s.find(temp) == s.end())
                s.insert(temp);
        }
        
        return s.size();
    }
};
```