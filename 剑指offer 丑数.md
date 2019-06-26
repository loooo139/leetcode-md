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
        int minValue=min(res[ugly2]*2,min(res[ugly3]*3,res[ugly5]*5));
        res[index++]=minValue;
        if(res[ugly2]*2==minValue)ugly2++;
        if(res[ugly3]*3==minValue)ugly3++;
        if=(res[ugly5]*5<=minValue)ugly5++;
    }
    return res.back();
}
```

```cpp
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> res(1, 1);
        int i2 = 0, i3 = 0, i5 = 0;
        while (res.size() < n) {
            int m2 = res[i2] * 2, m3 = res[i3] * 3, m5 = res[i5] * 5;
            int mn = min(m2, min(m3, m5));
            if (mn == m2) ++i2;
            if (mn == m3) ++i3;
            if (mn == m5) ++i5;
            res.push_back(mn);
        }
        return res.back();
    }
};
```

