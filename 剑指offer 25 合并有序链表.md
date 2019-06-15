# 剑指offer 25 合并有序链表

# [25. 合并两个排序的链表](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=_25-合并两个排序的链表)

[NowCoder](https://www.nowcoder.com/practice/d8b6b4358f774294a89de2a6ac4d9337?tpId=13&tqId=11169&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=题目描述-3)

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/c094d2bc-ec75-444b-af77-d369dfb6b3b4.png)

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 20~29?id=解题思路-5)

**迭代**

```cpp
ListNode * combineLists(ListNode *node1,ListNode *node2){
    if(node1==nullptr)return node2;
    if(node2==nullptr)return node1;
    ListNode *dummy=new ListNode(-1),*cur=dummy;
    while(node1&&node2){
        if(node1->val<node2->val){
            auto *temp=node1->next;
            node1->next=cur->next;
            cur->next=node1;
            cur=cur->next;
            node1=temp;
        }
        else{
            auto temp=node2->next;
            node2->next=cur->next;
            cur->next=node2;
            cur=cur->next;
            node2=temp;
        }
    }
    if(node1)cur->next=node1;
    if(node2)cur->next=node2;
    return dummy->next;
}
```

**递归**

```cpp
ListNode *combineLists(ListNode *node1,ListNode *node2){
    if(node1==nullptr)return node2;
    if(node2==nullptr)return node1;
    if(node1->val<=node2->val){
        auto *t=node1->next;
        node1->next=combineLists(t,node2);
        return node1;
    }
    else{
        auto *t=node2->next;
        node2->next=combineLists(t,node1);
        return node2;
    }
}
```

