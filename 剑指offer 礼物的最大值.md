# 剑指offer 礼物的最大值

# [47. 礼物的最大价值](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=_47-礼物的最大价值)

[NowCoder](https://www.nowcoder.com/questionTerminal/72a99e28381a407991f2c96d8cb238ab)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=题目描述-6)

在一个 m*n 的棋盘的每一个格都放有一个礼物，每个礼物都有一定价值（大于 0）。从左上角开始拿礼物，每次向右或向下移动一格，直到右下角结束。给定一个棋盘，求拿到礼物的最大价值。例如，对于如下棋盘

```
1    10   3    8
12   2    9    6
5    7    4    11
3    7    16   5
```

礼物的最大价值为 1+12+5+7+7+16+5=53。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=解题思路-8)

应该用动态规划求解，而不是深度优先搜索，深度优先搜索过于复杂，不是最优解。

``` cpp
int getMaxGifts(vector<vector<int>>matrix){
    int m=matrix.size();
    if(m==0)return 0;
    int n=matrix[0].size();
    vector<vector<int>>dp(m,vector<int>(n,0));
    for(int i=0;i<m;i++)
        for(int j=0;j<n;j++){
            int left=0,up=0;
            if(i>0)
                up=dp[i-1][j];
            if(j>0)
                left=dp[i][j-1];
            dp[i][j]=matrix[i][j]+max(left,right);
        }
    return dp[m-1][n-1];
}
```

**上面方法空间复杂度有点高**

**可以简化成o(n) 该数组的前j个数字为当前第i行前面j个礼物的最大数值，而之后的数字保存着第i-1行N-j
个格子礼物的最大值**

```cpp
int getMaxGifts(vector<vector<int>>matrix){
    int m=matrix.size();
    if(m==0)return 0;
    int n=matrix[0].size();
    vector<int>dp(n,0);
    for(int i=0;i<m;i++)
        for(int j=0;j<n;j++){
            int left=0,up=0;
            if(i>0)
                up=dp[j];
            if(j>0)
                left=dp[j-1];
            dp[j]=matrix[i][j]+max(left,right);
        }
    return dp[m-1][n-1];
}
```

