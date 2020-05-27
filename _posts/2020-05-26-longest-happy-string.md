---
title: Longest Happy String
author: Soubhik Rakshit
date: 2020-05-26 22:15:00 -0400
categories: [Leetcode, Code]
tags: [medium, priority queue]
---

[**LeetCode Question Link**](https://leetcode.com/problems/longest-happy-string/){:target="_blank"}

**Problem Statement**

> A string is called happy if it does not have any of the strings `'aaa'`, `'bbb'` or `'ccc'` as a substring.

> Given three integers `a`, `b` and `c`, return **any** string `s`, which satisfies following conditions:

> * `s` is _happy_ and longest possible.
> * `s` contains **at most** `a` occurrences of the letter `'a'`, **at most** `b` occurrences of the letter `'b'` and **at most** `c` occurrences of the letter `'c'`.
> * `s` will only contain `'a'`, `'b'` and `'c'` letters.

> If there is no such string `s` return the empty string `""`.

CONSTRAINTS:

1. `0 <= a, b, c <= 100`
2. `a + b + c > 0`

**Solution Approach**

* If a particular node is the root of the solution, then the maximum length of longest path is the sum of height of left and right subtree of the node. Otherwise, we pass the maximum height of left and right to the parent nodes.

**Complexity**

Let n be a+b+c.
* Time complexity - _O(n)_ to create string of size n.
* Space complexity - _O(1)_. Since, priority queue has only 3 items, space complexity is constant.

**Code**

```c++
class Solution {
public:
    string longestDiverseString(int a, int b, int c) {
        string result="";
        priority_queue<pair<int, char> > pq;
        if(a>0)
            pq.push({a, 'a'});
        if(b>0)
            pq.push({b, 'b'});
        if(c>0)
            pq.push({c, 'c'});
        
        int i=0;
        while(!pq.empty()) {
            pair<int, char> top = pq.top();
            pq.pop();
            if(i>1 && result[i-2]==top.second && result[i-1]==top.second) {
                if(pq.empty())
                    return result;
                pair<int, char> top2 = pq.top();
                pq.pop();
                result+=top2.second;
                if(top2.first>1)
                    pq.push({top2.first-1, top2.second});
                pq.push(top);
                i++;
            }
            else {
                result += top.second;
                if(top.first>1)
                    pq.push({top.first-1, top.second});
                i++;
            }
        }
        
        return result;
    }
};
```