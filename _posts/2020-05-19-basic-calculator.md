---
title: Basic Calculator
author: Soubhik Rakshit
date: 2020-05-19 15:00:00 -0400
categories: [Leetcode, Code]
tags: [hard, string]
---

[**LeetCode Question Link**](https://leetcode.com/problems/basic-calculator/){:target="_blank"}

**Problem Statement**

> Implement a basic calculator to evaluate a simple expression string.
> The expression string may contain open `(` and closing parentheses `)`, the plus `+` or minus sign `-`, **non-negative** integers and empty spaces .

NOTE:

1. You may assume that the given expression is always valid.
2. **Do not** use the `eval` built-in library function.

**Solution Approach**

* First tokenize the string. We insert `(` at the beginning and `)` at the end.
* Use stack to evaluate the expressions. Whenever we encounter `)` token, we evaluate the entire expression until we reach a `(` token. Then we replace the expression by its resulting value.

**Complexity**

Let `\|s\|` be the size of the stack.
* Time complexity - _O(\|s\|)_, as we need to parse entire input string.
* Space complexity - _O(\|s\|)_, to store the stack. However, I have used another _O(\|s\|)_ space to store the tokens separately. This was to make the program more intuitive. Overall, space complexity remains the same.

**Code**

```c++
class Solution {
public:
    int calculate(string s) {
        vector<string> tokens;
        tokens.push_back("(");
        for(int i=0; i<s.size(); i++) {
            if(s[i]=='(' || s[i]==')' || s[i]=='-' || s[i]=='+') {
                string temp(1, s[i]);
                tokens.push_back(temp);
            }
            else if(s[i]==' ')
                continue;
            else {
                int start = i;
                while(i<s.size()-1 && isdigit(s[i+1]))
                    i++;
                tokens.push_back(s.substr(start, i-start+1));
            }
        }
        
        tokens.push_back(")");
        
        stack<string> st;
        for(int i=0; i<tokens.size(); i++) {
            if(tokens[i]==")") {
                int result=0;
                int oprnd;
                
                string oprt = "", operand = "";
                
                operand = st.top();
                oprnd = stoi(operand);
                
                st.pop();
                
                while(st.top()!="(") {
                    oprt = st.top();
                    st.pop();
                    
                    if(oprt=="+")
                        result+=oprnd;
                    else
                        result-=oprnd;
                    
                    operand = st.top();
                    st.pop();
                    oprnd = stoi(operand);
                }
                
                result += oprnd;
                st.pop();
                st.push(to_string(result));
            }
            else
                st.push(tokens[i]);
        }
        
        return stoi(st.top());
    }
};
```