# 剑指offer [27. 二叉树的镜像](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=_27-二叉树的镜像)

[NowCoder](https://www.nowcoder.com/practice/564f4c26aa584921bc75623e48ca3011?tpId=13&tqId=11171&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=题目描述-5)

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/0c12221f-729e-4c22-b0ba-0dfc909f8adf.jpg)

> 输入一个二叉树，该函数输出它的镜像二叉树。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=解题思路-7)

**递归**

这种可以显然分为子问题的题目，使用递归求解是比较方便的

```cpp
void mirrorBinaryTree(TreeNode *node){
    if(node==nullptr)return;
    auto * left=node->left;
    node->left=node->right;
    node->right=left;
    mirrorBinaryTree(node->left);
    mirrorBinaryTree(node->right);
}
```

