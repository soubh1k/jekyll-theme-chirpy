---
title: Self Dividing Numbers
author: Soubhik Rakshit
date: 2020-06-17 14:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, array]
---

[**LeetCode Question Link**](https://leetcode.com/problems/self-dividing-numbers/){:target="_blank"}

**Problem Statement**

> A _self-dividing number_ is a number that is divisible by every digit it contains.

> For example, 128 is a self-dividing number because `128 % 1 == 0`, `128 % 2 == 0`, and `128 % 8 == 0`.

> Also, a self-dividing number is not allowed to contain the digit zero.

> Given a lower and upper number bound, output a list of every possible self dividing number, including the bounds if possible.

**Solution Approach**

* Brute force every number in the range to check if it is a self dividing number.

**Complexity**

* Time complexity - _O(right-left)_ to traverse the range of numbers.
* Space complexity - _O(right-left)_ to store the set of self dividing numbers.

**Code**

```c++
class Solution {
public:
    bool noZero(int n) {
        while(n>0) {
            if(n%10 == 0)
                return false;
            n /= 10;
        }
        return true;
    }
    
    vector<int> selfDividingNumbers(int left, int right) {
        vector<int> result;
        int temp;
        int rem;
        for(int num = left; num <= right; num++) {
            if(noZero(num)) {
                temp = num;
                while(temp>0) {
                    rem = temp%10;
                    if(num%rem != 0)
                        break;
                    temp/=10;
                }
                if(temp==0)
                    result.push_back(num);
            }
        }
        return result;
    }
};
```