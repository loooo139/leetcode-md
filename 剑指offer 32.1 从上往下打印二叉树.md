# 剑指offer [32.1 从上往下打印二叉树](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=_321-从上往下打印二叉树)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-2)

从上往下打印出二叉树的每个节点，同层节点从左至右打印。

例如，以下二叉树层次遍历的结果为：1,2,3,4,5,6,7

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/d5e838cf-d8a2-49af-90df-1b2a714ee676.jpg)

**层序遍历** 

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
    vector<int> PrintFromTopToBottom(TreeNode* root) {
        vector<int>res;
        queue<TreeNode*>q;
        if(!root)return res;
        q.push(root);
        while(!q.empty()){
            auto t=q.front();
            res.push_back(t->val);
            q.pop();
            if(t->left)q.push(t->left);
            if(t->right)q.push(t->right);
        }
        return res;
    }
};
```

