---
title: Rotate String
author: Soubhik Rakshit
date: 2020-06-11 11:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/rotate-string/){:target="_blank"}

**Problem Statement**

> We are given two strings, `A` and `B`.

> A _shift_ on `A` consists of taking string `A` and moving the leftmost character to the rightmost position. For example, if A = `'abcde'`, then it will be `'bcdea'` after one shift on `A`. Return `True` if and only if `A` can become `B` after some number of shifts on `A`.

NOTE: 

`A` and `B` will have length at most 100.

**Solution Approach**

* This problem can be solved by brute force in _O(n^2)_ time by comparing the two strings shifting one of them repeatedly by 1 until all shifted strings are compared.
* A better way to solve it is using KMP string matching algorithm. This algorithm requires extra space to store the array of numbers which counts _longest prefix which is also a suffix_ (**LPS**) up until that point in the array.
* Using the **LPS** array, we can skip matching prefixes as the prefix is equal to suffix and hence, the prefix can be safely taken out of consideration in case of mismatch.
* We repeat string B twice and try to find if string `A` can be found in the new string. This is similar to searching in a shifted array.

**Complexity**

Let m be the size of `A` and n be the size of `B`.
* Time complexity - _O(m+n)_, where _O(m)_ is required to construct the **LPS** array and O(n) is needed to traverse the entire string for pattern checking.
* Space complexity - _O(m+n)_, to store the **LPS** array and the new repeated string `B`.

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
    
    bool rotateString(string A, string B) {
        if(A.size()==0 && B.size()==0)
            return true;
        if(A.size() != B.size())
            return false;
        vector<int> lps_array = lps(A);
        string text = B+B;
        string pattern = A;
        int pos = find(text, pattern);
        
        return pos!=-1?true:false;
    }
};
```