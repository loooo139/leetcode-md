# 剑指offer 二叉搜索树与双向链表

# [36. 二叉搜索树与双向链表](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=_36-二叉搜索树与双向链表)

[NowCoder](https://www.nowcoder.com/practice/947f6eb80d944a84850b0538bf0ec3a5?tpId=13&tqId=11179&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-8)

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的双向链表。要求不能创建任何新的结点，只能调整树中结点指针的指向。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/05a08f2e-9914-4a77-92ef-aebeaecf4f66.jpg)

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=解题思路-8)

利用中序遍历

lastNode 指向前一个节点

```cpp
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    TreeNode* Convert(TreeNode* pRootOfTree)
    {
        TreeNode *lastNode=nullptr;
        ConvertRe(pRootOfTree,&lastNode);
        auto * head=lastNode;
        while(head&&head->left){
            head=head->left;
        }
        return head;        
    }
    void ConvertRe(TreeNode *node,TreeNode**last){
        if(node==nullptr)return;
        if(node->left)
            ConvertRe(node->left,last);
        node->left=*last;
        if((*last))
            (*last)->right=node;
        *last=node;
        if(node->right)
            ConvertRe(node->right,last);
    }
};
```

