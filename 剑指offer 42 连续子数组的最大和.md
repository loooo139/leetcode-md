# 剑指offer 42 连续子数组的最大和



## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=题目描述-2)

{6, -3, -2, 7, -15, 1, 2, 2}，连续子数组的最大和为 8（从第 0 个开始，到第 3 个为止）。



```cpp
class Solution {
public:
    int FindGreatestSumOfSubArray(vector<int> array) {
    int res=INT_MIN,sum=0;
        for(auto i:array){
            sum+=i;
            if(res<0&&i<0)res=max(res,i);
            if(sum<0)sum=0;
            else{
                res=max(res,sum);
            }
        }
        return res;
    }
};
```

### 动态规划

```cpp
class Solution {
public:
    int FindGreatestSumOfSubArray(vector<int> array) {
        int dp[array.size()],res=INT_MIN;
        for(int i=0;i<array.size();i++){
            if(i=0||dp[i-1]<0)
                dp[i]=array[i];
            else
                dp[i]=dp[i-1]+array[i];
            res=max(res,dp[i]);
        }
        return res;
    }
};
```

