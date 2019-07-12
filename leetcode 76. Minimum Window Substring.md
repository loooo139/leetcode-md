# leetcode 76. [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)

|  Category  |  Difficulty   | Likes | Dislikes |
| :--------: | :-----------: | :---: | :------: |
| algorithms | Hard (30.36%) | 2340  |   158    |

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Example:**

```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```

**Note:**

- If there is no such window in S that covers all characters in T, return the empty string `""`.
- If there is such window, you are guaranteed that there will always be only one unique minimum window in S.

这个题目是一个滑动串口的题目。假设S为ADBADC，T为ABC；我们需要先对模式串进行统计，统计出来每个字符出现的次数。然后对S串进行遍历。设置窗口左端点为0，然后开始遍历S，对于遇到的每一个字符先进行自减--，若自减后仍然大于1，则说明是T中的字符，cnt++。当cnt==T.size（）的时候说明我们找到了一个窗口的右端点，这时候的窗口大小可能不是最优解，所以移动左窗口，对每个字符进行自加若其值大于0说明该字符彻底从窗口中消失且该字符出现在T中顾需要cnt--。

```cpp
string minimumWindowSubstring(string S,string T){
    vector<int>nums(256,0);
    string res="";
    int left=0,cnt=0,minLen=INT_MAX;
    for(auto i:T)nums[i]++;
    for(int i=0;i<S.size();i++){
        if(--nums[S[i]]>=0){
            cnt++
        }
        while(cnt==T.size()){
            if(minLen>i-left+1){
                minLen=i-left+1;
                res=S.substr(left,minLen);
            }
            if(++nums[S[i]]>0)cnt--;
            left++;
        }
    }
    return res;
}
```

这个题目我刚开始没有想明白的地方在于存放字符出现次数的时候如何进行区分T中的字符。其实后来仔细想了想，滑动窗口向右扩张的时候，每次都--nums[char]，只有出现在T中的char才会nums[char]>=0,没有出现在T中的char值得范围是<0得，也就是说出现得nums[char]是>=1,而没有得为nums[char]==0.对于每个进入窗口得字符都进行自减，则会使没有出现在T中得char小于零。对于窗口内出现次数大于T中出现次数得char来说，其值也会小于零。左窗口边界收缩得时候对其值进行自加，只有其值大于零得说明该字符串在t中出现且不在窗口中了，此时cnt--；