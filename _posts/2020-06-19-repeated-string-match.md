---
title: Repeated String Match
author: Soubhik Rakshit
date: 2020-06-19 12:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/repeated-string-match/){:target="_blank"}

**Problem Statement**

> Given two strings A and B, find the minimum number of times A has to be repeated such that B is a substring of it. If no such solution, return -1.

> For example, with A = "abcd" and B = "cdabcdab".

> Return 3, because by repeating A three times (“abcdabcdabcd”), B is a substring of it; and B is not a substring of A repeated two times ("abcdabcd").

NOTE:

The length of `A` and `B` will be between 1 and 10000.

**Solution Approach**

* We repeat `A` until we reach the size atleast equal to `B`.
* If `A` and `B` are of the same size, we compare to see if they are equal.
* If not, we repeat `A` one more time and check if `B` can be found in `A` using KMP. This will return the number of repetitions if `A` is of the form `xB` or `Bx`, where `x` is any string.
* If not, we repeat `A` one more time and find `B` using KMP. This will return the number of repetitions if `A` is of the form `xBy`.
* Otherwise, we return -1.


**Complexity**

Let m be the size of `A` and n be the size of `B`.
* Time complexity - _O(m + n)_ to perform binary search.
* Space complexity - _O(n)_ to store LPS array during KMP search.

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
    
    int repeatedStringMatch(string A, string B) {
        if(A==B)
            return 1;
        string temp = A;
        int count = 1;
        while(A.size()<=B.size()) {
            A = A + temp;
            count++;
            if(A==B)
                return count;
        }
        
        int result = find(A, B);
        
        if(result == -1) {
            A = A+temp;
            count++;
        }
        
        result = find(A, B);
        
        return result==-1?-1:count;
    }
};
```