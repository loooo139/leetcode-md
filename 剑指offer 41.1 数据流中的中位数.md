# 剑指offer 41.1 数据流中的中位数

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=题目描述)

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=解题思路-1)

中位数一定存在，若总数组为偶数，则中位数为中间两个数字的平均值，那么可以将数组分为两个大小为数组大小一半的数组，左边存放较小的一半，右边存放较大的一半。可以遇见的是，左边需要关心的只有最大的数字，使用大顶堆即可，右边需要关心的是数组中最小的元素使用小顶堆就可。当数组长度为奇数的时候可以，中间数字可以分在左右任意一堆中，堆长度最大的那个堆顶就是中位数。

> **维护一个大顶堆，一个小顶堆，要求两堆的大小差距不超过1**

```cpp
priority_queue<int,vector<int>,less<int>>q;//左边的大顶堆
priority_queue<int,vector<int>,greater<int>>p;//右边的小顶堆；
class Solution {
public:
    priority_queue<int,vector<int>,less<int>>q;
    priority_queue<int,vector<int>,greater<int>>p;
    void Insert(int num)
    {
        
        if(q.empty()||num<=q.top())q.push(num);
        else p.push(num);
        if(q.size()>=p.size()+2){p.push(q.top());q.pop();}
        if(p.size()==q.size()+1){q.push(p.top());p.pop();}
    }

    double GetMedian()
    { 
       return q.size()==p.size()?(q.top()+p.top())/2.0:q.top();
    }

};
```

