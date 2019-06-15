# 剑指offer [32.2 把二叉树打印成多行](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=_322-把二叉树打印成多行)

> 将二叉树打印成多行

## 解题思路

```cpp
/*
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }
};
*/
class Solution {
public:
        vector<vector<int> > Print(TreeNode* pRoot) {
        vector<vector<int>>res;
            if(pRoot==nullptr)return res;
            queue<TreeNode*>q;
            q.push(pRoot);
            while(!q.empty()){
                int size=q.size();
                vector<int>line;
                for(int i=0;i<size;i++){
                    auto *temp=q.front();
                    q.pop();
                    line.push_back(temp->val);
                    if(temp->left)q.push(temp->left);
                    if(temp->right)q.push(temp->right);
                }
                res.push_back(line);
            }
            return res;
        }
    
    
};
```

# [32.3 按之字形顺序打印二叉树](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=_323-按之字形顺序打印二叉树)

[NowCoder](https://www.nowcoder.com/practice/91b69814117f4e8097390d107d2efbe0?tpId=13&tqId=11212&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-4)

请实现一个函数按照之字形打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右至左的顺序打印，第三行按照从左到右的顺序打印，其他行以此类推。

```cpp
/*
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }
};
*/
class Solution {
public:
    vector<vector<int> > Print(TreeNode* pRoot) {
        vector<vector<int>>res;
        if(pRoot==nullptr)return res;
        queue<TreeNode*>q;
        q.push(pRoot);
        bool flag=false;
        while(!q.empty()){
            int size=q.size();
            vector<int>line;
            for(int i=0;i<size;i++){
                auto *temp=q.front();
                line.push_back(temp->val);
                q.pop();
                if(temp->left)q.push(temp->left);
                if(temp->right)q.push(temp->right);
            }
            if(flag)
                reverse(line.begin(),line.end());
            flag=!flag;
            res.push_back(line);
        }
        return res;
    }
    
};
```

