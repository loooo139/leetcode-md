# 剑指offer [29. 顺时针打印矩阵](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=_29-顺时针打印矩阵)

[NowCoder](https://www.nowcoder.com/practice/9b4c81a02cd34f76be2659fa0d54342a?tpId=13&tqId=11172&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=题目描述-7)

下图的矩阵顺时针打印结果为：1, 2, 3, 4, 8, 12, 16, 15, 14, 13, 9, 5, 6, 7, 11, 10

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/48517227-324c-4664-bd26-a2d2cffe2bfe.png)

采用四个坐标来控制运动的方向，顺时针进行运动。条件判断

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=解题思路-9)

```cpp
void printMatrix(vector<vector<int>>matrix){
    vector<int> res;
    int m=matrix.size(),n=matrix[0].size();
    int left=0,right=n-1,up=0,down=m-1;
    while(true){
        for(int i=left;i<=right;i++)
            res.push_back(matrix[up][i]);
        up++;
        if(up>down) break;
        for(int i=up;i<=down;i++)
            res.push_back(matrix[i][right]);
        right--;
        if(left>right) break;
        for(int i=right;i>=left;i--)
            res.push_back(matrix[down][i]);
        down--;
        if(up>down)break;
        for(int i=down;i>=up;i--)
            res.push_back(matrix[i][left]);
        left++;
        if(left>right)break;
    }
}
```