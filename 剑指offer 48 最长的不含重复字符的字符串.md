# 剑指offer 48 最长的不含重复字符的字符串

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=题目描述-7)

输入一个字符串（只包含 a~z 的字符），求其最长不含重复字符的子字符串的长度。例如对于 arabcacfr，最长不含重复字符的子字符串为 acfr，长度为 4。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=解题思路-9)

### 滑动窗口+hashmap

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int>dict(256,-1);
        int maxlen=0,left=-1;
        for(int i=0;i<s.size();i++){
            if(dict[s[i]]>left){
                left=dict[s[i]];
            }
            dict[s[i]]=i;
            maxlen=max(maxlen,i-left);
        }
        return maxlen;
    }
};
```



```cpp
   /**
     * @brief  第二种方法 动态规划
     * @note   
     * @param  s: 
     * @retval 
     */
    int lengthOfLongestSubstring(string s)
    {
        vector<int> dict(256, -1);
        if (s.empty())
            return 0;
        int res = INT_MIN;
        int curLength = 0;
        for (int i = 0; i < s.size(); i++)
        {
            if (i == 0 || curLength + dict[s[i]] < i)
                curLength++;
            else
            {
                curLength = i - dict[s[i]];
            }
            res = max(res, curLength);
            dict[s[i]] = i;
        }
        return res;
    }
};
```



