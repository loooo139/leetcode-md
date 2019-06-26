# leetcode  5.[Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

Given a string **s**, find the longest palindromic substring in **s**. You may assume that the maximum length of **s** is 1000.

**Example 1:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: "cbbd"
Output: "bb"
```

本题目要求找到一个字符串的最长回文子串，对于一个回文子串来说，是一个中心对称的子串。最简单的方法就是对每个子字符为中心，像两边阔寻。然后找出最大值即可。这种的时间复杂度为`O(n^2)`.
```cpp
string longestPalindromic(string s){
    int start=0,len=0,n=s.size();
    for(int i=0;i<n;i++){
        find(s,i,i,start,len);
        find(s,i,i+1,start,len);
    }
    return s.substr(start,len);
}
void find(string s,int left,int right,int &start,int &len){
    if(right>=s.size())return;
    while(left>=0&&right<s.size()&&s[left]==s[right]){
        left--;right++;
    }
    if(right-left-1>len){
        len=right-left-1;
        start=left+1;
    }
}
 
```

除此之外还可以使用动态规划来做。我们维护一个二维数组 dp，其中 dp[i][j] 表示字符串区间 [i, j] 是否为回文串，当 i = j 时，只有一个字符，肯定是回文串，如果 i = j + 1，说明是相邻字符，此时需要判断 s[i] 是否等于 s[j]，如果i和j不相邻，即 i - j >= 2 时，除了判断 s[i] 和 s[j] 相等之外，dp[i + 1][j - 1] 若为真，就是回文串，通过以上分析，可以写出递推式如下：

dp[i, j] = 1                                               if i == j

​           = s[i] == s[j]                                if j = i + 1

​           = s[i] == s[j] && dp`[i + 1][j - 1] `   if j > i + 1      

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        if (s.empty()) return "";
        int dp[s.size()][s.size()] = {0}, left = 0, right = 0, len = 0;
        for (int i = 0; i < s.size(); ++i) {
            dp[i][i] = 1;
            for (int j = 0; j < i; ++j) {
                dp[j][i] = (s[i] == s[j] && (i - j < 2 || dp[j + 1][i - 1]));
                if (dp[j][i] && len < i - j + 1) {
                    len = i - j + 1;
                    left = j;
                    right = i;
                }
            }
        }
        return s.substr(left, right - left + 1);
    }
};
```

最后一种也是最牛逼的，可以用O(n)的时间复杂度来完成的马拉车算法。具体的连接这是一篇专门介绍马拉车算法的博客 [Manacher's Algorithm 马拉车算法](http://www.cnblogs.com/grandyang/p/4475985.html)

```cpp
class Solution {
public:
    string longestPalindrome(string s) {
    string t = "$#";
    for (int i = 0; i < s.size(); ++i) {
        t += s[i];
        t += "#";
    }
    // Process t
    int p[t.size()]={0};
    int mx = 0, id = 0, resLen = 0, resCenter = 0;//mx指最大的回文串对应的右端点，id为最大的回文串的中心点，reslen是指回文对称的长度，resCenter就是对称中心。
    for (int i = 1; i < t.size(); ++i) {
        p[i] = mx > i ? min(p[2 * id - i], mx - i) : 1;//这里是该算法的核心问题，主要是利用之前已经遍历到回文串的性质：对称。直接获取到该点的对称长度。
        while (t[i + p[i]] == t[i - p[i]]) ++p[i];
        if (mx < i + p[i]) {
            mx = i + p[i];
            id = i;
        }
        if (resLen < p[i]) {
            resLen = p[i];
            resCenter = i;
        }
    }
    return s.substr((resCenter - resLen) / 2, resLen - 1);
    }
};
```

