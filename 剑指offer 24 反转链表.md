# 剑指offer 24 反转链表

反转链表

## 递归

```cpp
ListNode * reverseLinkList(ListNode * node){
    if(node==nullptr||node->next==nullptr)
        return node;
    ListNode *next=reverseLinkList(node->next);
    node->next->next=node;
    node->next=nullptr;
    return next;
}
```

## 迭代

/头插法/

```cpp
ListNode *reverseLinkList(ListNode *node){
    ListNode *dummy=new ListNode(-1);
    dummy->next=nullptr;
    while(node){
        auto * temp=node->next;
        node->next=dummy->next;
        dummy->next=node;
        node=temp;
    }
    return dummy->next;
}
```

