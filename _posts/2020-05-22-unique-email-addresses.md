---
title: Unique Email Addresses
author: Soubhik Rakshit
date: 2020-05-22 12:00:00 -0400
categories: [Leetcode, Code]
tags: [easy, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/last-stone-weight-ii/){:target="_blank"}

**Problem Statement**

> Every email consists of a local name and a domain name, separated by the @ sign.
> For example, in `alice@leetcode.com`, `alice` is the local name, and `leetcode.com` is the domain name.
> Besides lowercase letters, these emails may contain `'.'`s or `'+'`s.
> If you add periods (`'.'`) between some characters in the **local name** part of an email address, mail sent there will be forwarded to the same address without dots in the local name.  For example, `"alice.z@leetcode.com"` and `"alicez@leetcode.com"` forward to the same email address.  (Note that this rule does not apply for domain names.)
> If you add a plus (`'+'`) in the **local name**, everything after the first plus sign will be **ignored**. This allows certain emails to be filtered, for example `m.y+name@email.com` will be forwarded to `my@email.com`.  (Again, this rule does not apply for domain names.)
> It is possible to use both of these rules at the same time.
> Given a list of `emails`, we send one email to each address in the list.  How many different addresses actually receive mails? 

**Solution Approach**

* Initialize a set to store all unique emails.
* Split email into local and domain names.
* Remove text after `+` from local name.
* Remove `.` from local name.
* Join names
* Add to set
* Return size of set.

**Complexity**

Let n be the number of emails and \|s\| be the maximum size of an email.
* Time complexity - _O(n\|s\|)_. 
* Space complexity - _O(\|s\|)_, to store the domain and local part of an email.

**Code**

```c++
class Solution {
public:
    int numUniqueEmails(vector<string>& emails) {
        unordered_set<string> uniqueEmails;
        for(int i=0; i<emails.size(); i++) {
            string currEmail = emails[i];
            
            // Split local name and domain name
            int j=0;
            while(j<currEmail.size() && currEmail[j]!='@')
                j++;
            string localName = currEmail.substr(0, j);
            string domainName = currEmail.substr(j+1);
            
            // Ignore text after + in local name
            int plus_index = 0;
            while(plus_index<localName.size() && localName[plus_index]!='+')
                plus_index++;
            localName = localName.substr(0, plus_index);
            
            // Ignore dots in local name
            int dot_index = 0;
            while(dot_index<localName.size()) {
                if(localName[dot_index]=='.')
                    localName.erase(dot_index, 1);
                else
                    dot_index++;
            } 
            
            // Join names
            string newEmail = localName + "@" + domainName;
            
            // Add to set
            uniqueEmails.insert(newEmail);
        }
        return uniqueEmails.size();
    }
};
```