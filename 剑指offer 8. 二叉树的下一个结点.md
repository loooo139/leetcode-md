# 剑指offer [8. 二叉树的下一个结点](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 3~9?id=_8-二叉树的下一个结点)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 3~9?id=题目描述-5)

给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点的指针。

```java
public class TreeLinkNode {

    int val;
    TreeLinkNode left = null;
    TreeLinkNode right = null;
    TreeLinkNode next = null;

    TreeLinkNode(int val) {
        this.val = val;
    }
}
```

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 3~9?id=解题思路-5)

① 如果一个节点的右子树不为空，那么该节点的下一个节点是右子树的最左节点；

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/b0611f89-1e5f-4494-a795-3544bf65042a.gif)

② 否则，向上找第一个左链接指向的树包含该节点的祖先节点。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/95080fae-de40-463d-a76e-783a0c677fec.gif)

```cpp
Node * findNext(Node *node){
    if(node==nullptr)return nullptr;
    if(node->right){
        node=node->right;
        while(node->left)
            node=node->left;
        return node;
    }else{
        while(node->next&&node->next->left!=node)
            node=node->next;
        return node->next;
    }
}
```

