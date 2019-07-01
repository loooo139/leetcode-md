# leetcode 32[Longest Valid Parentheses](https://leetcode.com/problems/longest-valid-parentheses/description/)

|  Category  |  Difficulty   | Likes | Dislikes |
| :--------: | :-----------: | :---: | :------: |
| algorithms | Hard (25.23%) | 1913  |    91    |

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

```
Input: "(()"
Output: 2
Explanation: The longest valid parentheses substring is "()"
```

**Example 2:**

```cpp
{Input: ")()())"
Output: 4
Explanation: The longest valid parentheses substring is "()()"}
```

本题目是要求最长的有效括号。括号匹配的题目大概率是使用栈来解决，左括号进栈，右括号出栈。本题目是要求最长长度，因此括号里面要放入的应该是括号的位置。当遇到的字符串是左括号时候，入栈存入位置，当遇到右括号时：若此时栈为空，则当前位置不可能是一个匹配的起点，left=i+1,否则出栈顶元素，查看栈是否为空，为空len=i-left+1，不然len=i-st.top（）；

```cpp
class Solution{
    public:
    int LongestValidParentheses(string s){
        int res=0,left=0,n=s.size();
        stack<int>st;
        for(int i=0;i<n;i++){
            if(s[i]=='(')st.push_back(i);
            else if(s[i]==')'){
                if(st.empty()) left=i+1;
                else{
                    st.pop();
                    int len=st.empty()?i-left+1:i-st.top();
                    res=max(res,len);
                }
            }
        }
        return res;
    }
}
```



