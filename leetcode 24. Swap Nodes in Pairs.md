# leetcode 24. Swap Nodes in Pairs

------

Given a linked list, swap every two adjacent nodes and return its head.

**Example:**

```
Given 1->2->3->4, you should return the list as 2->1->4->3.
```

**Note:**

- Your algorithm should use only constant extra space.
- You may **not** modify the values in the list's nodes, only nodes itself may be changed.

```c++
ListNode* swapPairs(ListNode *head){
    ListNode* dummy=new ListNode(-1),*cur=dummy;
    cur->next=head;
    while(cur->next&&cur->next->next){
        ListNode *t=cur->next->next;
        cur->next->next=t->next;
        t->next=cur->next;
        cur->next=t;
        cur=t->next;
    }
    return dummy->next;
}
```



