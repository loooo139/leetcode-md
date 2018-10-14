# leetcode 3 

Given a string, find the length of the **longest substring** without repeating characters.

**Example 1:**

```
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
```

**Example 2:**

```
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
```

**Example 3:**

```
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not
```

```c++
int lengthOfLongestSubstring(string s){
    int m[300]={0};
    int res=0,left=0;
    for(int i=0;i<s.size();i++){
        if(m[s[i]]==0||m[s[i]]<left){
            res=max(res,i-left+1);
        }
        else
            left=m[s[i]];
    }
    return res;
}
```

