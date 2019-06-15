# 剑指offer 26. 树的子结构

[NowCoder](https://www.nowcoder.com/practice/6e196c44c7004d15b1610b9afca8bd88?tpId=13&tqId=11170&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=题目描述-4)

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/84a5b15a-86c5-4d8e-9439-d9fd5a4699a1.jpg)

>输入两个树节点a,b，判断b树是否是a的子结构。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=解题思路-6)

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
    bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2)
    {
        if(!pRoot1||!pRoot2)
            return false;
        return isHasSubtree(pRoot1,pRoot2)||HasSubtree(pRoot1->left,pRoot2)||HasSubtree(pRoot1->right,pRoot2);
    }
    bool isHasSubtree(TreeNode * pt1,TreeNode * pt2){
        if(!pt2)return true;
        if(!pt1)return false;
        
        if(pt1->val!=pt2->val)return false;
        return isHasSubtree(pt1->left,pt2->left)&&isHasSubtree(pt1->right,pt2->right);
    }
};
```

