---
title: Longest Palindrome
author: Soubhik Rakshit
date: 2020-05-25 14:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/longest-palindrome/){:target="_blank"}

**Problem Statement**

> Given a string which consists of lowercase or uppercase letters, find the length of the longest palindromes that can be built with those letters.

> This is case sensitive, for example `"Aa"` is not considered a palindrome here.

NOTE:

Assume the length of given string will not exceed 1,010.

**Solution Approach**

* Count frequency of all characters. Atmost 1 character can have odd frequency to make a palindromic string.
* For every character with even frequency, we increment `count` by that frequency.
* For every character with odd frequency, we increment `count` by that frequency decremented by 1.
* Finally, if there was a character with odd frequency, we increment count by 1.

**Complexity**

Let \|s\| be size of input string.
* Time complexity - _O(|s|)_ to traverse the entire string and the HashMap.
* Space complexity - _O(|s|)_ to store the HashMap.

**Code**

```c++
class Solution {
public:
    int longestPalindrome(string s) {
        unordered_map<char, int> m;
        for(int i=0; i<s.size(); i++) {
            if(m.find(s[i])!=m.end())
                m[s[i]]++;
            else
                m[s[i]]=1;
        }
        
        int count = 0;
        int maxOdd = 0;
        for(auto it=m.begin(); it!=m.end(); it++) {
            if(it->second%2==0)
                count+=it->second;
            else {
                count+=it->second-1;
                maxOdd = 1;
            }
        }
        return count + maxOdd;
    }
};
```