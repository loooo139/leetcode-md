# 剑指offer 46 把数字翻译成字符串

# [46. 把数字翻译成字符串](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=_46-把数字翻译成字符串)

[Leetcode](https://leetcode.com/problems/decode-ways/description/)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=题目描述-5)

给定一个数字，按照如下规则翻译成字符串：1 翻译成“a”，2 翻译成“b”... 26 翻译成“z”。一个数字有多种翻译可能，例如 12258 一共有 5 种，分别是 abbeh，lbeh，aveh，abyh，lyh。实现一个函数，用来计算一个数字有多少种不同的翻译方法。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=解题思路-7)

### 动态规划

dp[i]=dp[i-1]//str[i-1]!='0'

dp[i]=0//str[i-1]==0;

dp[i]+=dp[i-2]//str[i-1:i-2]>=10,<=26;

```cpp
class Solution {
public:
    int numDecodings(string s) {
        if (s.empty()) return 0;
        vector<int> dp(s.size() + 1, 0);
        dp[0] = 1;
        for (int i = 1; i < dp.size(); ++i) {
            if (s[i - 1] != '0') dp[i] += dp[i - 1];
            if (i >= 2 && s.substr(i - 2, 2) <= "26" && s.substr(i - 2, 2) >= "10") {
                dp[i] += dp[i - 2];
            }
        }
        return dp.back();
    }
};
```

