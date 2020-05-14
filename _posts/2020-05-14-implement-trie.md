---
title: Implement Trie (Prefix Tree)
author: Soubhik Rakshit
date: 2020-05-14 12:00:00 -0400
categories: [Leetcode, Code]
tags: [medium, tree, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/implement-trie-prefix-tree/){:target="_blank"}

**Problem Statement**

> Implement a trie with `insert`, `search`, and `startsWith` methods.

NOTE:
1. You may assume that all inputs are consist of lowercase letters `a`-`z`.
2. All inputs are guaranteed to be non-empty strings.

**Solution Approach**

* Initialiaze the trie by creating a `head` node. Every node in the trie contains a vector of 26 child nodes. Initially, the children of `head` are `NULL`.
* There is also a boolean variable `present` which denotes whether the word ending at that particular node should be in the trie or not.
* For `insert` operation, we check if corresponding characters are present in the trie or not. If they are, we simply proceed to the next character. Otherwise, we create a new child to trie. Finally, we reach the end of the stirng and set `present` to `true` denoting the fact that the string ending at that node is present in the trie.
* For `search` operation, we simply check if corresponding children of the nodes are present in the trie or not. If we cannot find a child for any character in the string, we return `false`. Otherwise, we traverse the trie until we reach the end of the string. Finally, we check if the value of `present` in the node is `true` or not. If not, then that word was never inserted into the trie. Otherwise we return `true`.
* For `startsWith` operation, we perform the same operation as in `search`. However, if we are able to reach the end of the string while traversing the trie, we return `true` else `false`.

**Complexity**

### Tree Initialization
* Time complexity - _O(1)_
* Space compexity - _O(1)_

### insert
Let n be the size of string.
* Time complexity - _O(n)_
* Space compexity - _O(n)_

### search
Let n be the size of string.
* Time complexity - _O(n)_
* Space compexity - _O(1)_

### startsWith
Let n be the size of prefix
* Time complexity - _O(n)_
* Space compexity - _O(1)_

**Code**

```c++
class TrieNode {
    public:
    char val;
    vector<TrieNode *> children;
    bool present;
    TrieNode(char val) {
        children.resize(26, NULL);
        this->val = val;
        present=false;
    }
};

class Trie {
public:
    TrieNode* head;
    /** Initialize your data structure here. */
    Trie() {
        TrieNode *temp = new TrieNode(0);
        head = temp;
    }
    
    /** Inserts a word into the trie. */
    void insert(string word) {
        TrieNode* temp = head;
        for(int i=0; i<word.size(); i++) {
            if(temp->children[word[i]-'a']==NULL) {
                TrieNode *node = new TrieNode(word[i]);
                temp->children[word[i]-'a'] = node;
                temp = temp->children[word[i]-'a'];
            }
            else {
                temp = temp->children[word[i]-'a'];
            }
        }
        temp->present = true;
    }
    
    /** Returns if the word is in the trie. */
    bool search(string word) {
        TrieNode* temp = head;
        for(int i=0; i<word.size(); i++) {
            if(temp->children[word[i]-'a']==NULL)
                return false;
            temp = temp->children[word[i]-'a'];
        }
        if(temp->present==true)
            return true;
        return false;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    bool startsWith(string prefix) {
        TrieNode* temp = head;
        for(int i=0; i<prefix.size(); i++) {
            if(temp->children[prefix[i]-'a']==NULL)
                return false;
            temp = temp->children[prefix[i]-'a'];
        }
        return true;
    }
};

/**
 * Your Trie object will be instantiated and called as such:
 * Trie* obj = new Trie();
 * obj->insert(word);
 * bool param_2 = obj->search(word);
 * bool param_3 = obj->startsWith(prefix);
 */
```

**Further extensions**

* This program can be extended by creating a `delete` function which can remove words from the trie.
* This would involve a lot more effort by making sure that there are no empty branches present in the original trie after the `delete` operation.
* If you want to contribute, feel free to send a pull request in [**Github**](https://github.com/soubh1k/blog).