# leetcode 25. Reverse Nodes in k-Group

Given a linked list, reverse the nodes of a linked list *k* at a time and return its modified list.

*k* is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of *k* then left-out nodes in the end should remain as it is.



**Example:**

Given this linked list: `1->2->3->4->5`

For *k* = 2, you should return: `2->1->4->3->5`

For *k* = 3, you should return: `3->2->1->4->5`

**Note:**

- Only constant extra memory is allowed.
- You may not alter the values in the list's nodes, only nodes itself may be changed.

## Recursive

```c++
ListNode * reverseKGroup(ListNode *head,int k){
    ListNode *cur=head;
    for(int i=0;i<k;i++){
        if(!cur) return head;
        cur=cur->next;
    }
    ListNode * new_head=reverse(head,cur);
    head->next=reversKGroup(cur,k);
    return new_head;
}
ListNode * reverse(ListNode *head,ListNode * tail){
    ListNode *pre=tail;
    while(head!=tail){
        ListNode *t = head->next;
        head->next=pre;
        pre=head;
        head=t;
    }
    return pre;
}
```



## iteraterive

```c++   
ListNode * reverseKGroup(ListNode *head,int k){
    ListNode*dummy=new ListNode(-1),*pre=dummy,*cur=pre;
    dummy->next=head;
    int num=0;
    while(cur=cur->next) num++;
    while(num>=k){
        cur=pre->next;
        for(int i=1;i<k;i++){
            ListNode *t =cur->next;
            cur->next=t->next;
            t->next=pre->next;
            pre->next=t;
        }
        pre=cur;
        num-=k;
    }
    return dummy->next;
    
}
```

