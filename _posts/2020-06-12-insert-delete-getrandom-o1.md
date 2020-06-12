---
title: Insert Delete GetRandom O(1)
author: Soubhik Rakshit
date: 2020-06-12 12:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, hashing]
---

[**LeetCode Question Link**](https://leetcode.com/problems/insert-delete-getrandom-o1/){:target="_blank"}

**Problem Statement**

> Design a data structure that supports all following operations in _average_ **O(1)** time.

1. `insert(val)`: Inserts an item val to the set if not already present.
2. `remove(val)`: Removes an item val from the set if present.
3. `getRandom`: Returns a random element from current set of elements. Each element must have the **same probability** of being returned.

**Solution Approach**

* This problem can be solved using the _Set_ data structure. More specifically, we use _unordered\_set_ as it provides element access, removal and modification in constant time.
* Insertion and removal is straightforward. We check if the element is already present, perform the operation in the set and return `true` or `false` accordingly.
* We use a random number generator `r` to generate a uniform random number between `0` and `s.size()-1`.
* We return the element after advancing `r` times from the beginning of the _unordered\_set_.

**Complexity**

Let n be the maximum number of values inserted into the set.
* Time complexity - _O(1)_ for all operations.
* Space complexity - _O(n)_ is required for storing the set.

**Code**

```c++
class RandomizedSet {
public:
    /** Initialize your data structure here. */
    unordered_set<int> s;
    RandomizedSet() {
        srand(time(NULL));
    }
    
    /** Inserts a value to the set. Returns true if the set did not already contain the specified element. */
    bool insert(int val) {
        if(s.find(val)==s.end()) {
            s.insert(val);
            return true;
        }
        return false;
    }
    
    /** Removes a value from the set. Returns true if the set contained the specified element. */
    bool remove(int val) {
        if(s.find(val)==s.end())
            return false;
        s.erase(val);
        return true;
    }
    
    /** Get a random element from the set. */
    int getRandom() {
        int r = rand()%s.size();
        auto it = s.cbegin();
        advance(it, r);
        return *it;
    }
};

/**
 * Your RandomizedSet object will be instantiated and called as such:
 * RandomizedSet* obj = new RandomizedSet();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```