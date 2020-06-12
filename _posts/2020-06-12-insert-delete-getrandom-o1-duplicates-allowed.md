---
title: Insert Delete GetRandom O(1) - Duplicates allowed
author: Soubhik Rakshit
date: 2020-06-12 13:00:00 -0400
categories: [Leetcode, Code]
tags: [hard, hashing]
---

[**LeetCode Question Link**](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/){:target="_blank"}

**Problem Statement**

> Design a data structure that supports all following operations in _average_ **O(1)** time.

> **Note: Duplicate elements are allowed.**

1. `insert(val)`: Inserts an item val to the collection.
2. `remove(val)`: Removes an item val from the collection if present.
3. `getRandom`: Returns a random element from current collection of elements. The probability of each element being returned is **linearly related** to the number of same value the collection contains.

**Solution Approach**

* This problem can be solved using the _Multiset_ data structure. Multiple instances of the same object can be present in a Multiset.
* Multiset provides provides element access, removal and modification in constant time.
* Insertion and removal is straightforward. We check if the element is already present, perform the operation in the multiset and return `true` or `false` accordingly.
* We use a random number generator `r` to generate a uniform random number between `0` and `s.size()-1`.
* We return the element after advancing `r` times from the beginning of the _unordered\_multiset_.

**Complexity**

Let n be the maximum number of values inserted into the set.
* Time complexity - _O(1)_ for all operations.
* Space complexity - _O(n)_ is required for storing the set.

**Code**

```c++
class RandomizedCollection {
public:
    /** Initialize your data structure here. */
    unordered_multiset<int> ms;
    RandomizedCollection() {
        srand(time(NULL));
    }
    
    /** Inserts a value to the collection. Returns true if the collection did not already contain the specified element. */
    bool insert(int val) {
        if(ms.find(val)==ms.end()) {
            ms.insert(val);
            return true;
        }
        ms.insert(val);
        return false;
    }
    
    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    bool remove(int val) {
        if(ms.find(val)==ms.end())
            return false;
        auto it = ms.find(val);
        ms.erase(it);
        return true;
    }
    
    /** Get a random element from the collection. */
    int getRandom() {
        int r = rand()%ms.size();
        auto it = ms.cbegin();
        advance(it, r);
        return *it;
    }
};

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection* obj = new RandomizedCollection();
 * bool param_1 = obj->insert(val);
 * bool param_2 = obj->remove(val);
 * int param_3 = obj->getRandom();
 */
```