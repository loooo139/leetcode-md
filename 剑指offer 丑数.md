# 剑指offer 丑数

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=题目描述-8)

把只包含因子 2、3 和 5 的数称作丑数（Ugly Number）。例如 6、8 都是丑数，但 14 不是，因为它包含因子 7。习惯上我们把 1 当做是第一个丑数。求按从小到大的顺序的第 N 个丑数。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=解题思路-10)

```cpp
int getUglyNumber(int n){
    vector<int>res(n);
    if(n<=0)return -1;
    res[0]=1;
    int index=1;
    int ugly2=0,ugly3=0,ugly5=0;
    while(index<n){
        int minValue=min(ugly2*2,min(ugly3*3,ugly5*5));
        res[index++]=minValue;
        while(res[ugly2]*2<=minValue)ugly2++;
        while(res[ugly3]*3<=minValue)ugly3++;
        while(res[ugly5]*5<=minValue)ugly5++;
    }
    return res.back();
}
```

