---
title: 1-bit and 2-bit Characters
author: Soubhik Rakshit
date: 2020-05-16 19:30:00 -0400
categories: [Leetcode, Code]
tags: [easy, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/1-bit-and-2-bit-characters/){:target="_blank"}

**Problem Statement**

> We have two special characters. The first character can be represented by one bit `0`. The second character can be represented by two bits (`10` or `11`).
> Now given a string represented by several bits. Return whether the last character must be a one-bit character or not. The given string will always end with a zero.

NOTE:
1. `1 <= len(bits) <= 1000`.
2. `bits[i]` is always `0` or `1`.

**Solution Approach**

* This is a pretty simple problem. We start traversing the array from the beginning. If we read `0`, we know element is 1 bit and if we read `1` we increment the traversal index by one and we know that this would be a 2 bit number.
* We return the final result as `true` if 1 bit or `false` otherwise.

**Complexity**

* Time complexity - _O(n)_. We need to traverse the entire vector once.
* Space complexity - _O(1)_. 

```c++
class Solution {
public:
    bool isOneBitCharacter(vector<int>& bits) {
        bool bit = false;
        for(int i=0; i<bits.size(); i++) {
            if(bits[i]==0) {
                bit=true;
            }
            else {
                bit=false;
                i++;
            }
        }
        return bit;
    }
};
```