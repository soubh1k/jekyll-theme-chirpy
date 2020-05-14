---
title: Add Binary
author: Soubhik Rakshit
date: 2020-05-13 23:30:00 -0400
categories: [Leetcode, Code]
tags: [easy, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/add-binary/){:target="_blank"}

**Problem Statement**

> Given two binary strings, return their sum (also a binary string).
> The input strings are both **non-empty** and contains only characters `1` or `0`.

**Solution Approach**

* I have written a very verbose version of the code which helps in understanding it better.
* Initialized a _carry_ with 0.
* Started adding the last bits in each string and adding the carry to it.
* This goes on until the control reaches the start of any string.
* There can be 3 cases on adding the two bits and the _carry_.
* If the sum is 3, we add `1` to `res` and set `carry` equal to `1`.
* If the sum is 2, we add `0` to `res` and set `carry` equal to `1`.
* If the sum is 1, we add `1` to `res` and set `carry` equal to `0`.
* Once we reach the end of the smaller array, we add the remaining elements into `res` keeping track of the _carry_ as well.
* Since, we append bits to the start of `res`, we don't need to reverse the resulting string.

**Complexity**

Let _m_ and _n_ be the size of the input arrays.
* Time complexity - _O(max(m, n))_, as we traverse once through the larger array.
* Space complexity - _O(max(m, n))_, as result will be almost the same size as that of the larger array.

**Code**

```c++
class Solution {
public:
    string addBinary(string a, string b) {
        int carry=0;
        int i=a.size()-1, j=b.size()-1;
        string result="";
        while(i>=0 && j>=0) {
            int sum=carry+(a[i]-'0') + (b[j]-'0');
            if(sum==3) {
                result="1"+result;
                carry=1;
            }
            else if(sum==2) {
                result="0"+result;
                carry=1;
            }
            else if(sum==1) {
                result="1"+result;
                carry=0;
            }
            else
                result="0"+result;
            
            i--;
            j--;
        }
        while(i>=0) {
            int sum = carry+a[i]-'0';
            if(sum==3) {
                result="1"+result;
                carry=1;
            }
            else if(sum==2) {
                result="0"+result;
                carry=1;
            }
            else if(sum==1) {
                result="1"+result;
                carry=0;
            }
            else
                result="0"+result;
            i--;
        }
        while(j>=0) {
            int sum = carry+b[j]-'0';
            if(sum==3) {
                result="1"+result;
                carry=1;
            }
            else if(sum==2) {
                result="0"+result;
                carry=1;
            }
            else if(sum==1) {
                result="1"+result;
                carry=0;
            }
            else
                result="0"+result;
            j--;
        }
        if(carry)
            result="1"+result;
        return result;
    }
};
```