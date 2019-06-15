# 剑指offer 38 字符串的排列

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-10)

输入一个字符串，按字典序打印出该字符串中字符的所有排列。例如输入字符串 abc，则打印出由字符 a, b, c 所能排列出来的所有字符串 abc, acb, bac, bca, cab 和 cba。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=解题思路-10)

### 方法一：DFS

```cpp
class Solution {
public:
    vector<string> Permutation(string str) {
        vector<bool>flag(256,false);
        vector<string>res;
        if(str.size()==0)return res;
        string temp;
        sort(str.begin(),str.end());
        DFS(res,temp,str,flag);
        return res;
    }
    void DFS(vector<string> &res,string &temp,string str,vector<bool>&flag){
        if(temp.size()==str.size()){
            res.push_back(temp);
            return;
        }
        for(int i=0;i<str.size();i++){
            if(!flag[i]){
                if(i!=0&&str[i]==str[i-1]&&!flag[i-1])continue;//保证在相同两个字符出现时，挑选第二个，第一个字符已经选择过应该跳过。
                temp.push_back(str[i]);
                flag[i]=true;
                DFS(res,temp,str,flag);
                temp.pop_back();
                flag[i]=false;
            }
        }
    }
};
```

### 方法二：交换

```cpp
class Solution {
public:
    vector<string> Permutation(string str) {
        //string temp(str.begin(),str.end());
        vector<string>res;
        if(str.size()==0)return res;
        sort(str.begin(),str.end());
        helper(res,str,0);
        return res;
    }
    void helper(vector<string>&res,string&str,int start){
        if(start>=str.size())res.push_back(str);
        for(int i=start;i<str.size();i++){
            if(i!=start&&str[i]==str[start])continue;
            swap(str[i],str[start]);
            helper(res,str,start+1);
            swap(str[i],str[start]);
        }
    }
};
```

解法二：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        set<vector<int>> res;
        permute(nums, 0, res);
        return vector<vector<int>> (res.begin(), res.end());
    }
    void permute(vector<int>& nums, int start, set<vector<int>>& res) {
        if (start >= nums.size()) res.insert(nums);
        for (int i = start; i < nums.size(); ++i) {
            if (i != start && nums[i] == nums[start]) continue;
            swap(nums[i], nums[start]);
            permute(nums, start + 1, res);
            swap(nums[i], nums[start]);
        }
    }
};
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

对于上面的解法，你可能会有疑问，我们不是在swap操作之前已经做了剪枝了么，为什么还是会有重复出现，以至于还要用TreeSet来取出重复呢。总感觉使用TreeSet去重复有点耍赖，可能并没有探究到本题深层次的内容。这是很好的想法，首先我们先尝试将上面的TreeSet还原为vector，并且在主函数调用递归之前给nums排个序（代码参见评论区三楼），然后测试一个最简单的例子：[1, 2, 2]，得到的结果为：

[[1,2,2], [2,1,2], [2,2,1], [2,2,1],  [2,1,2]]

我们发现有重复项，那么我们的剪枝究竟在做些什么，怎么还是没法防止重复项的产生！我们的那个剪枝只是为了防止当 start = 1, i = 2 时，将两个2交换，这样可以防止 {1, 2, 2} 被加入两次。但是没法防止其他的重复情况，要闹清楚为啥，我们需要仔细分析一些中间过程，下面打印了一些中间过程的变量：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
start = 0, i = 0 => {1 2 2} 
start = 1, i = 1 => {1 2 2} 
start = 2, i = 2 => {1 2 2} 
start = 3 => saved  {1 2 2}
start = 1, i = 2 => {1 2 2} skipped
start = 0, i = 1 => {1 2 2} -> {2 1 2}
start = 1, i = 1 => {2 1 2} 
start = 2, i = 2 => {2 1 2} 
start = 3 => saved  {2 1 2}
start = 1, i = 2 => {2 1 2} -> {2 2 1}
start = 2, i = 2 => {2 2 1} 
start = 3 => saved  {2 2 1}
start = 1, i = 2 => {2 2 1} -> {2 1 2} recovered
start = 0, i = 1 => {2 1 2} -> {1 2 2} recovered
start = 0, i = 2 => {1 2 2} -> {2 2 1}
start = 1, i = 1 => {2 2 1} 
start = 2, i = 2 => {2 2 1} 
start = 3 => saved  {2 2 1}
start = 1, i = 2 => {2 2 1} -> {2 1 2}
start = 2, i = 2 => {2 1 2} 
start = 3 => saved  {2 1 2}
start = 1, i = 2 => {2 1 2} -> {2 2 1} recovered
start = 0, i = 2 => {2 2 1} -> {1 2 2} recovered
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

问题出在了递归调用之后的还原状态，参见上面的红色的两行，当 start = 0, i = 2 时，nums 已经还原到了 {1, 2, 2} 的状态，此时 nums[start] 不等于 nums[i]，我们的剪枝在这已经失效了，那么交换后的 {2, 2, 1} 还会被存到结果res中，而这个状态我们在之前就已经存过了一次。

我们注意到当 start = 0, i = 1 时，nums交换之后变成了 {2, 1, 2}，如果我们能保持这个状态，那么当 start = 0, i = 2 时，此时 nums[start] 就等于 nums[i] 了，我们的剪枝操作就可以发挥作用了。怎么才能当递归结束后，不还原成为交换之前的状态的呢？答案就是不进行还原，这样还是能保存为之前交换后的状态。我们只是将最后一句 swap(nums[i], nums[start]) 删掉是不行的，因为我们的递归函数的参数 nums 是加了&号，就表示引用了，那么之前调用递归函数之前的 nums 在递归函数中会被修改，可能还是无法得到我们想要的顺序，所以我们要把递归函数的nums参数的&号也同时去掉才行，参见代码如下：

 

解法三：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
class Solution {
public:
    vector<vector<int>> permuteUnique(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        permute(nums, 0, res);
        return res;
    }
    void permute(vector<int> nums, int start, vector<vector<int>>& res) {
        if (start >= nums.size()) res.push_back(nums);
        for (int i = start; i < nums.size(); ++i) {
            if (i != start && nums[i] == nums[start]) continue;
            swap(nums[i], nums[start]);
            permute(nums, start + 1, res);
        }
    }
};
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

好，我们再测试下 [1, 2, 2] 这个例子，并且把中间变量打印出来：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
start = 0, i = 0 => {1 2 2} 
start = 1, i = 1 => {1 2 2} 
start = 2, i = 2 => {1 2 2} 
start = 3 => saved  {1 2 2}
start = 1, i = 2 => {1 2 2} skipped
start = 0, i = 1 => {1 2 2} -> {2 1 2}
start = 1, i = 1 => {2 1 2} 
start = 2, i = 2 => {2 1 2} 
start = 3 => saved  {2 1 2}
start = 1, i = 2 => {2 1 2} -> {2 2 1}
start = 2, i = 2 => {2 2 1} 
start = 3 => saved  {2 2 1}
start = 1, i = 2 => {2 2 1} recovered
start = 0, i = 1 => {2 1 2} recovered
start = 0, i = 2 => {2 1 2} skipped
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

明显发现短了许多，说明我们的剪枝发挥了作用，我们看上面红色部分，当 start = 0, i = 1 时，递归函数调用完了之后，nums数组保持了 {2, 1, 2} 的状态，那么到 start = 0, i = 2 的时候，nums[start] 就等于 nums[i] 了，我们的剪枝操作就可以发挥作用了。

这时候你可能会想，调用完递归不恢复状态，感觉怪怪的，跟哥的递归模版不一样啊，容易搞混啊，而且一会加&号，一会不加的，这尼玛谁能分得清啊。别担心，I gotcha covered! 好，既然还是要恢复状态的话，我们就只能从剪枝入手了，原来那种naive的剪枝方法肯定无法使用，矛盾的焦点还是在于，当 start = 0, i = 2 时，nums被还原成了 start = 0, i = 1 的交换前的状态 {1, 2, 2}，这个状态已经被处理过了，再去处理一定会产生重复，我们怎么才知道这被处理过了呢，当前的 i = 2，我们需要往前去找是否有重复出现，由于数组已经排序过了，如果有重复，那么前面数一定和当前的相同，所以我们用一个while循环，往前找和 nums[i] 相同的数字，找到了就停下，当然如果小于start了也要停下，那么如果没有重复数字的话，j 一定是等于 start-1 的，那么如果不等于的话，就直接跳过就可以了，这样就可以去掉所有的重复啦，参见代码如下：