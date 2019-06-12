# 剑指offer 4 二维数组中的查找

>给定一个二维数组，其每一行从左到右递增排序，从上到下也是递增排序。给定一个数，判断这个数是否在该二维数组中。

```html
Consider the following matrix:
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]

Given target = 5, return true.
Given target = 20, return false.
```

# 解题思路

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/0ad9f7ba-f408-4999-a77a-9b73562c9088.gif)

时间复杂度为O(m+n),空间复杂度为常数。

```cpp
bool findMatrix(vector<vector<int>>matrix,int target){
    if (matrix == null || matrix.size() == 0 || matrix[0].sieze() == 0)
        return false;
    int m=matrix.size(),n=matrix[0].size();
    int i=0,j=n-1;
    while(i<m&&j>=0){
        if(matrix[i][j]==traget)
            return true;
        else if(matrix[i][j]>target)
            j--;
        else
            i++;
    }
    return false;
}
```

