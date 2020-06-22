---
title: To Lower Case
author: Soubhik Rakshit
date: 2020-06-16 14:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/to-lower-case/){:target="_blank"}

**Problem Statement**

> Implement function ToLowerCase() that has a string parameter str, and returns the same string in lowercase.

**Solution Approach**

* Used lambda function in C++ STL `std::transform` to transform string to lowercase.

**Complexity**

Let s be the size of the string.
* Time complexity - _O(s)_ to traverse the string.
* Space complexity - _O(1)_ as the string is transformed in place.

**Code**

```c++
class Solution {
public:
    string toLowerCase(string str) {
        transform(str.begin(), str.end(), str.begin(), [](char c) {
            return tolower(c);
        });
        return str;
    }
};
```