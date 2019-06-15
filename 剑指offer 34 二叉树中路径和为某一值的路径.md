# 剑指offer 34 二叉树中路径和为某一值的路径

# [34. 二叉树中和为某一值的路径](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=_34-二叉树中和为某一值的路径)

[NowCoder](https://www.nowcoder.com/practice/b736e784e3e34731af99065031301bca?tpId=13&tqId=11177&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-6)

输入一颗二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

下图的二叉树有两条和为 22 的路径：10, 5, 7 和 10, 12

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/ed77b0e6-38d9-4a34-844f-724f3ffa2c12.jpg)

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=解题思路-6)

DFS

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
    vector<vector<int> > FindPath(TreeNode* root,int expectNumber) {
	vector<vector<int>>res;
    vector<int>path;
     if(root==nullptr)return res;
     DFS(root,expectNumber,res,path);
     return res;
    }
    void DFS(TreeNode *root,int num,vector<vector<int>>&res,vector<int>path){
        if(root==nullptr||root->val>num)return ;
        num-=root->val;
        path.push_back(root);
        if(num==0&&root->left==nullptr&&root->right==nullptr)
            res.push_back(path);
        DFS(root->left,num,res,path);
        DFS(root->right,num,res,path);
        path.pop_back();
        
    }
};
```

