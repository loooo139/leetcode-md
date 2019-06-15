# 剑指offer  [28 对称的二叉树](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=_28-对称的二叉树)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=题目描述-6)

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/0c12221f-729e-4c22-b0ba-0dfc909f8adf.jpg)

> 判断一个二叉树是不是对称的

**递归 **

```cpp
bool isSymmetrical(TreeNode * node){
    if(node==nullptr)return true;
    judge(node->left,node->right);
}
bool judge(TreeNode *left,TreeNode *right){
    if(left==nullptr&&right==nullptr)
        return true;
    if(!left||!right)return false;
    if(left->val!+right->val)return false;
    return judge(left->left,right->right)&&judge(left->right,rihgt->left);
}
```

