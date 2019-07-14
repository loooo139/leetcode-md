# leetcode专题总结 -二分搜索

最近做了不少题目，感觉比较有套路就是*动态规划*和*二分搜索*。其中二分搜索因为存在模板，原理简单很多人自以为搞明白，搞清楚了这个算法。但在刷题的过程中发现边界条件，左右区间的初始化上存在很多大的差别。我刷题的时候去看别人解答的时候是一脸的懵逼。今天有空就把二分搜索好好的总结下：

## 二分搜索

优点：

1. 高效 时间复杂度为`O(logn)`级别

缺点：

1. 只适用于有序数组

二分搜索根据左右区间初始化的不同分为许多的版本，其不同之处在于左右区间以及循环条件上。十分容易记混，我个人常用的模板是区间[m,n],即双端闭区间。比如要在范围1到50内搜索，我的初始区间则为[1，50]。与之对应的则是循环条件为l<=right;

```cpp
//二分搜索模板
int binarySearch(int left,int right){
    int left=left,right=right;
    while(left<=right){
        int mid=left+(right-left)/2; //防止溢出
        //g(x)为各个具体题目的具体要求判断函数
        if(g(mid))
        	right=mid-1;
        else
            left=mid+1;
        
    }
    return left;
    
}
```

二分搜索的难点在于g(x)的定义，注意尽量不要在循环里面判断返回，容易出错。可以记住返回的是满足g(x)的最小值，而不是直接对g(x)进行求解。

![1562771635547](https://raw.githubusercontent.com/loooo139/leetcode-md/master/asset/1562771635547.png)

![1562771672480](https://raw.githubusercontent.com/loooo139/leetcode-md/master/asset/1562771672480.png)

![1563108721740](https://raw.githubusercontent.com/loooo139/leetcode-md/master/asset/1563108721740.png)

![1563110269832](E:\personal\2019\asset\1563110269832.png)

![1563110343648](https://raw.githubusercontent.com/loooo139/leetcode-md/master/asset/1562771635547.png)