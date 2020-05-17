---
title: Find All Anagrams in a String
author: Soubhik Rakshit
date: 2020-05-17 11:30:00 -0400
categories: [Leetcode, Code]
tags: [medium, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/find-all-anagrams-in-a-string/){:target="_blank"}

**Problem Statement**

> Given a string `s` and a **non-empty** string `p`, find all the start indices of `p`'s anagrams in `s`.
> Strings consists of lowercase English letters only and the length of both strings `s` and `p` will not be larger than 20,100.
> The order of output does not matter.

**Solution Approach**
* We use a sliding window technique by maintaining a HashMap containing frequency of characters in the window.
* First we count the frequency of characters in `p` and store it in the HashMap `m`. Then we subtract the character frequency in `s` using a window size the same size as `p`.
* Next, we keep sliding the window while removing the left element from `m` and adding the new element. We check if the current window forms an anagram and repeat this step until the window reaches end of `s`.


**Complexity**

Let |s| be the length of s.
* Time complexity - _O(|s|)_, as `s` is the larger array and we traverse it entirely once.
* Space complexity - _O(|s|)_, Hashmap stores sum of every pair of elements.

**Code**

```c++
class Solution {
public:
    bool checkAnagram(unordered_map<char, int> &m) {
        for(auto it=m.begin(); it!=m.end(); it++) {
            if(it->second!=0)
                return false;
        }
        return true;
    }
    vector<int> findAnagrams(string s, string p) {
        vector<int> result;
        if(s.size()==0 || p.size()==0 || s.size()<p.size())
            return result;
        
        unordered_map<char, int> m;
        for(int i=0; i<p.size(); i++) {
            if(m.find(p[i])!=m.end())
                m[p[i]]++;
            else
                m[p[i]]=1;
            
            if(m.find(s[i])!=m.end())
                m[s[i]]--;
            else
                m[s[i]]=-1;
        }
        if(checkAnagram(m))
            result.push_back(0);
        
        for(int i=1; i<s.size()-p.size()+1; i++) {
            m[s[i-1]]++;
            if(m.find(s[i+p.size()-1])==m.end())
                m[s[i+p.size()-1]]=-1;
            else
                m[s[i+p.size()-1]]--;
            
            if(checkAnagram(m))
                result.push_back(i);
        }
        
        return result;
    }
};
```