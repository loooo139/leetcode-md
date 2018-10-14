# leetcode 22. Generate Parentheses

Given *n* pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given *n* = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

```c++
class Solution {
public:
    vector<string> generateParenthesis(int n) {
        vector<string> res;
        generater(n,n,"",res);
        return res;
        
    }
    void generater(int left,int right,string out,vector<string>& res){
        if(left>right) return;
        if(left==0&&right==0) res.push_back(out);
        if(left)generater(left-1,right,out+'(',res);
        if(right)generater(left,right-1,out+')',res);
    }
};
```

