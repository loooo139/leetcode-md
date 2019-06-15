# 剑指offer [37. 序列化二叉树](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=_37-序列化二叉树)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-9)

请实现两个函数，分别用来序列化和反序列化二叉树。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=解题思路-9)

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
    string Serialize(TreeNode *root) {    
        ostringstream out;
        serialize(root,out);
        return out.str();
    }
    TreeNode* Deserialize(string str) {
    	istringstream in(str);
        return deserialize(in);
    }
private:
    void serialize(TreeNode *root,ostringstream &out){
        if(root==nullptr)
            out<<'#';
        else{
            out<<out->val<<' ';
            serialize(root->left,out);
            serialize(root->right,out);
        }
    }
    TreeNode* deserialize(istringstream &in){
        string val;
        in>>val;
        if(val=='#')
            return nullptr;
        TreeNode *temp=new TreeNode(stoi(val));
        temp->left=deserialize(in);
        temp->right=deserialize(in);
        return temp;
    }
};
```

