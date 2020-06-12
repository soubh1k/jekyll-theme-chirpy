---
title: Implement Queue using Stacks
author: Soubhik Rakshit
date: 2020-06-10 12:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, stack, queue]
---

[**LeetCode Question Link**](https://leetcode.com/problems/implement-queue-using-stacks/){:target="_blank"}

**Problem Statement**

> Implement the following operations of a queue using stacks.

1. push(x) -- Push element x to the back of queue.
2. pop() -- Removes the element from in front of queue.
3. peek() -- Get the front element.
4. empty() -- Return whether the queue is empty.

**Solution Approach**

* Use two stacks.
* We store all elements in the first stack.
* The second stack is used temporarily to reach the end of the stack during dequeuing and peeking.

**Complexity**

* Time complexity - _O(1)_ for pushing new element and checking whether array is empty.
* Space complexity - _O(n)_ for dequeuing and peeking the front of the queue.

**Code**

```c++
class MyQueue {
public:
    /** Initialize your data structure here. */
    stack<int> s1;
    stack<int> s2;
    
    MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    void push(int x) {
        s1.push(x);
    }
    
    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        while(!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
        int result = s2.top();
        s2.pop();
        while(!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
        return result;
    }
    
    /** Get the front element. */
    int peek() {
        while(!s1.empty()) {
            s2.push(s1.top());
            s1.pop();
        }
        int result = s2.top();
        while(!s2.empty()) {
            s1.push(s2.top());
            s2.pop();
        }
        return result;
    }
    
    /** Returns whether the queue is empty. */
    bool empty() {
        return s1.empty();
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */
```

**Final thoughts**

This code can be modified to have _O(1)_ amortized space for dequeuing and peeking by maintaining the same different stacks. However, we need to empty the second stack and store all elements back into the first stack on dequeuing and peeking.