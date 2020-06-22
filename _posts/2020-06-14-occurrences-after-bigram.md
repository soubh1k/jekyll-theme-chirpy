---
title: Occurrences After Bigram
author: Soubhik Rakshit
date: 2020-06-14 12:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/occurrences-after-bigram/){:target="_blank"}

**Problem Statement**

> Given words `first` and `second`, consider occurrences in some `text` of the form "`first second third`", where `second` comes immediately after `first`, and `third` comes immediately after `second`.

For each such occurrence, add "`third`" to the answer, and return the answer.

**Solution Approach**

* We check every word in the string and check if it is the same as `first`. If it is then we check if the next word is `second`. 
* Then we store the next word in the result only if the word atleast has 1 character.

**Complexity**

Let n be the size of string.
* Time complexity - _O(n)_ for traversing the string. We assume that size of any word is much smaller than the string itself.
* Space complexity - _O(n)_ to store the result.

**Code**

```c++
class Solution {
public:
    vector<string> findOcurrences(string text, string first, string second) {
        int i=0, j=0;
        
        vector<string> result;
        
        while(j<text.size()) {
            if(text[j]==' ') {
                
                if(text.substr(i, j-i)==first) {
                    cout<<i<<" "<<j<<endl;
                    int k = j+1;
                    while(k<text.size() && text[k]!=' ')
                        k++;
                    
                    if(text.substr(j+1, k-(j+1))==second) {
                        int l = k+1;
                        while(l<text.size() && text[l]!=' ')
                            l++;
                        if(l-(k+1)>0) {
                            result.push_back(text.substr(k+1, l-(k+1)));
                        }
                    }
                }
                i = j+1;
            }
            j++;
        }
        
        return result;
    }
};
```