# leetcode 19. Remove Nth Node From End of List

Given a linked list, remove the *n*-th node from the end of list and return its head.

**Example:**

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

**Note:**

Given *n* will always be valid.

**Follow up:**

Could you do this in one pass?

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode*dummy=new ListNode(-1);
        dummy->next=head;
        ListNode* right=dummy,*left=dummy;
        while(n--) left=left->next;
        while(left->next){
            left=left->next;
            right=right->next;
        }
        right->next=right->next->next;
        return dummy->next;
    }
};
```

