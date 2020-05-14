---
title: Add Strings
author: Soubhik Rakshit
date: 2020-05-13 00:00:00 +0000
categories: [Leetcode, Tutorial]
tags: [leetcode, easy]
---

[**Add Strings**](https://leetcode.com/problems/add-strings/)

**Problem Statement**
> Given two non-negative integers `num1` and `num2` represented as string, return the sum of `num1` and `num2`.

NOTE:
1. The length of both `num1` and `num2` is < 5100.
2. Both `num1` and `num2` contains only digits `0-9`.
3. Both `num1` and `num2` does not contain any leading zero.
4. You **must not use any built-in BigInteger library** or **convert the inputs to integer** directly.

```c++
class Solution {
public:
    string addStrings(string num1, string num2) {
        string res="";
        int i=0;
        int carry=0;
        int temp;
        while(i<num1.size() && i<num2.size()) {
            temp = num1[num1.size()-1-i]-'0' + num2[num2.size()-1-i]-'0' + carry;
            if(temp>9) {
                temp-=10;
                carry=1;
            }
            else
                carry=0;
            res+=to_string(temp);
            i++;
        }
        if(num1.size()>num2.size()) {
            while(i<num1.size()) {
                temp = num1[num1.size()-1-i]-'0' + carry;
                if(temp>9) {
                    temp-=10;
                    carry=1;
                }
                else
                    carry=0;
                res+=to_string(temp);
                i++;
            }
        }
        if(num2.size()>num1.size()) {
            while(i<num2.size()) {
                temp = num2[num2.size()-1-i]-'0' + carry;
                if(temp>9) {
                    temp-=10;
                    carry=1;
                }
                else
                    carry=0;
                res+=to_string(temp);
                i++;
            }
        }
        if(carry)
            res+="1";
        
        reverse(res.begin(), res.end());
        return res;
    }
};
```