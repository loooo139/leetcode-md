# 剑指offer 41.2字符流中第一个不重复的字符

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=题目描述-1)

请实现一个函数用来找出字符流中第一个只出现一次的字符。例如，当从字符流中只读出前两个字符 "go" 时，第一个只出现一次的字符是 "g"。当从该字符流中读出前六个字符“google" 时，第一个只出现一次的字符是 "l"。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=解题思路-2)

```cpp
class Solution
{
public:
    int hashmap[256];
    int i=1;
  //Insert one char from stringstream
    void Insert(char ch)
    {
         if(hashmap[ch]==-1)
             hashmap[ch]=i;
        else hashmap[ch]=0;
        i++;
    }
    Solution();
  //return the first appearence once char in current stringstream
    char FirstAppearingOnce()
    {
    	char res;int index=INT_MAX;
        for(int i=0;i<256;i++){
            if(hashmap[i]==-1||hashmap[i]==0)
                continue;
            else if(hashmap[i]<index){
                index=hashmap[i];
                res=i;
            }
        }
        if(index==INT_MAX)return '#';
        return res;
    }

};
Solution::Solution(){
    for(int i=0;i<256;i++)
        hashmap[i]=-1;
}
```

