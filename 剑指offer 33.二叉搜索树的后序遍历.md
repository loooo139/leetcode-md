# 剑指offer 33.二叉搜索树的后序遍历

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-5)

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。假设输入的数组的任意两个数字都互不相同。

例如，下图是后序遍历序列 1,3,2 所对应的二叉搜索树。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/13454fa1-23a8-4578-9663-2b13a6af564a.jpg)

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=解题思路-5)

二叉搜索树的特点是左节点的数值比根节点的小，右节点的数值比根节点的大。中序遍历生成的节点是递增的序列。而后序遍历，先遍历左右节点，最后才遍历根节点。根据二叉搜索树的特点，会得到根节点在最后，前面是左节点小于根节点的值，后半部分是右节点大于根节点的数值。

```cpp
bool judge(vector<int>numbers){
    if(numbers.size()==0)
        return false;
    return verify(numbers,0,numbers.size()-1);
}
bool verify(vector<int>numbers,int left,int right){
    if(left>=right)return true;
    int val=numbers[right],i=left,j=--right;
    while(numbers[i]<val)i++;
    while(numbers[j]>val)j--;
    if(i<j)return false;
    else return verify(numbers,0,j)&&verify(numbers,i,right);
}
```

