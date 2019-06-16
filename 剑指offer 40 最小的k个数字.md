# 剑指offer 40 最小的k个数字

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=解题思路)

[快速选择](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=快速选择)

- 复杂度：O(N) + O(1)
- 只有当允许修改数组元素时才可以使用

快速排序的 partition() 方法，会返回一个整数 j 使得 a[l..j-1] 小于等于 a[j]，且 a[j+1..h] 大于等于 a[j]，此时 a[j] 就是数组的第 j 大元素。可以利用这个特性找出数组的第 K 个元素，这种找第 K 个元素的算法称为快速选择算法。

```cpp
vector<int> kSmallest(vector<int>numbers,int k){
    vector<int>res;
    if(k==0||k>numbers.size())return res;
    int start=0,end=k-1,t=k-1;
    int index=partition(numbers,start,end);
    while(index!=t){
        if(index>t){
            end=index-1;
            index=partitin(numbers,start,end);
        }
        else{
            start=index+1;
            index=partition(numbers,start,end);
        }
    }
    return vector<int>(numbers.begin(),numbers.begin+k);
}
int partition(vector<int>&numbers,int start,int end){
    if(start>=end)return start;
    int val=numbers[start];
    while(start<end){
        while(start<end&&numbers[end]>=val)end--;
        numbers[left]=numbers[right];
        while(start<end&&numbers[left]<temp)left++;
        numbers[right]=numbers[left];
    }
    numbers[left]=temp;
    return left;
}
```

### [大小为 K 的最小堆](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=大小为-k-的最小堆)

- 复杂度：O(NlogK) + O(K)
- 特别适合处理海量数据



使用大顶堆来维护最小堆，大顶堆的top元素为k个元素的最大值，维护一个大小为k的大顶堆，就可。

```cpp
class Solution {
public:
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        vector<int>res;
        if(k<=0||k>input.size())return res;
        priority_queue<int,vector<int>,less<int>>q;
        for(int i=0;i<input.size();i++){
            if(q.size()<k)
                q.push(input[i]);
            else{
                if(q.top()>input[i]){
                    q.pop();
                    q.push(input[i]);
                }
            }
        }
        ;
        while(!q.empty()){
            res.push_back(q.top());
            q.pop();
        }
        return res;
        
    }
};
```

```cpp
class Solution {
public:
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        priority_queue<int,vector<int>,greater<int>>q;
        for(auto i:input)
            q.push(i);
        vector<int>res;
        while(!q.empty()&&(res.size()<k)){
            int i=q.top();q.pop();
            if(!res.empty()&&i==res.back())continue;
            else res.push_back(i);
        }
        if(res.size()<k)return {};
        else return res;
    }
};
```

