# leetcode  14. Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

**Example 1:**

```
Input: ["flower","flow","flight"]
Output: "fl"
```

**Example 2:**

```
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.
```

**Note:**

All given inputs are in lowercase letters `a-z`.

## 解题思路

> 公共前缀一定是最短字符串的一部分，对字符每个进行匹配即可

```c++
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        string res="";
        if(len(strs)==1)return strs[0];
        for(int i=0;i<str[0].size();i++){
            for(int j=1;j<len(strs);j++){
                if(str[0][i]!=str[j][i]||i>j)
                    return res;
            }
            res.push_back(str[0][i]);
        }
        return res;
};
```

```c
class Solution {
public:
    string longestCommonPrefix(vector<string>& strs) {
        if (strs.empty()) return "";
        string res = "";
        for (int j = 0; j < strs[0].size(); ++j) {
            char c = strs[0][j];
            for (int i = 1; i < strs.size(); ++i) {
                if (j >= strs[i].size() || strs[i][j] != c) {
                    return res;
                }
            }
            res.push_back(c);
        }
        return res;
    }
};
```

