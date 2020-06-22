---
title: Permutation Sequence
author: Soubhik Rakshit
date: 2020-06-20 11:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/permutation-sequence/){:target="_blank"}

**Problem Statement**

> The set `[1,2,3,...,n]` contains a total of _n!_ unique permutations.

> By listing and labeling all of the permutations in order, we get the following sequence for _n = 3_:

> 1. `"123"`
> 2. `"132"`
> 3. `"213"`
> 4. `"231"`
> 5. `"312"`
> 6. `"321"`

> Given _n_ and _k_, return the k<sup>th</sup> permutation sequence.

NOTE:

* Given _n_ will be between 1 and 9 inclusive.
* Given _n_ will be between 1 and _n!_ inclusive.

**Solution Approach**

* The solution to the problem is so well explained in [**this article**](https://leetcode.com/problems/permutation-sequence/discuss/22507/%22Explain-like-I'm-five%22-Java-Solution-in-O(n)){:target="_blank"} that it would be better to read it there.

**Complexity**

Let n be the number of operations.
* Time complexity - _O(n)_ to traverse all the operations.
* Space complexity - _O(1)_ as we don't use any extra space.

**Code**

```c++
class Solution {
public:
    int fact(int n) {
        if(n==0) return 1;
        else return fact(n-1) * n;
    }
    
    string getPermutation(int n, int k) {
        string nums = "";
        for(int i=1; i<=n; i++)
            nums += to_string(i);
        
        k--;

        string result = "";
        while(!nums.empty()) {
            int q = k/(fact(nums.size()-1));
            int r = k%(fact(nums.size()-1));
            
            result += nums[q];
            nums.erase(nums.begin()+q);
            
            k = r;
        }
        
        return result;
    }
};
```