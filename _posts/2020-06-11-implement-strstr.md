---
title: Implement strStr()
author: Soubhik Rakshit
date: 2020-06-11 12:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/implement-strstr/){:target="_blank"}

**Problem Statement**

> Implement strStr().

> Return the index of the first occurrence of `needle` in `haystack`, or -1 if `needle` is not part of `haystack`.

CLARIFICATION:

What should we return when needle is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when needle is an empty string. This is consistent to C's strstr() and Java's indexOf().

**Solution Approach**

* This problem is similar to that of [**Rotate String**]({{site.url}}/posts/rotate-string/). It can be solved by brute force in _O(n^2)_ time by comparing the two strings by searching the `needle` in the `haystack`.
* A better way to solve it is using KMP string matching algorithm. This algorithm requires extra space to store the array of numbers which counts _longest prefix which is also a suffix_ (**LPS**) up until that point in the array.
* Using the **LPS** array, we can skip matching prefixes as the prefix is equal to suffix and hence, the prefix can be safely taken out of consideration in case of mismatch.

**Complexity**

Let m be the size of A and n be the size of B.
* Time complexity - _O(m+n)_, where _O(m)_ is required to construct the **LPS** array and O(n) is needed to traverse the entire string for pattern checking.
* Space complexity - _O(m)_, to store the **LPS** array for the `needle`.

**Code**

```c++
class Solution {
public:
    vector<int> lps(string A) {
        vector<int> lps_array(A.size(), 0);
        int j=0;
        for(int i=1; i<A.size(); i++) {
            if(A[i]==A[j]) {
                lps_array[i] = lps_array[i-1] + 1;
                j++;
            }
            else {
                while(j>0 && A[i]!=A[j]) {
                    j--;
                    j = lps_array[j];
                }
                if(A[i]==A[j]) {
                    lps_array[i] = lps_array[j] + 1;
                    j++;
                }
                else
                    lps_array[i] = 0;
            }
        }
        return lps_array;
    }
    
    int find(string text, string pattern) {
        vector<int> lps_array = lps(pattern);
        
        int i=0, j=0;
        while(i<text.size() && j<pattern.size()) {
            if(text[i]==pattern[j]) {
                i++;
                j++;
            }
            else {
                while(j>0 && text[i]!=pattern[j]) {
                    j--;
                    j = lps_array[j];
                }
                if(text[i]==pattern[j]) {
                    i++;
                    j++;
                }
                else {
                    i++;
                }
            }
            if(j==pattern.size())
                return i-j;
        }
        return -1;
    }
    int strStr(string haystack, string needle) {
        if(needle=="")
            return 0;
        int result = find(haystack, needle);
        return result!=-1?result:-1;
    }
};
```