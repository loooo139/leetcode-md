# 剑指offer 6.从尾到头打印链表

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 3~9?id=题目描述-3)

从尾到头反过来打印出每个结点的值。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/f5792051-d9b2-4ca4-a234-a4a2de3d5a57.png)

## 解题思路

可以使用递归，也可以使用栈的先进后出特性来解决

```cpp
void reversePrint(ListNode * node){
    if(node==nullptr)return;
    reversePrint(node->next);
    print(node->val);
}
```

使用栈

```cpp
void reversePrint(ListNode *node){
    stack<int>res;
    while(node){
        res.push(node->val);
        node=node->next;
    }
    while(!res.empty()){
        print(res.top());
        res.pop();
    }
}
```

