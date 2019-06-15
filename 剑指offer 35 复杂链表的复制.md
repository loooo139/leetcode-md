# 剑指offer 35 复杂链表的复制

[NowCoder](https://www.nowcoder.com/practice/f836b2c43afc4b35ad6adc41ec941dba?tpId=13&tqId=11178&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-7)

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针指向任意一个节点），返回结果为复制后复杂链表的 head。

```cpp
struct RandomListNode {
    int label;
    struct RandomListNode *next, *random;
    RandomListNode(int x) :
            label(x), next(NULL), random(NULL) {
    }
};
```

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/66a01953-5303-43b1-8646-0c77b825e980.png)

```cpp
/*
struct RandomListNode {
    int label;
    struct RandomListNode *next, *random;
    RandomListNode(int x) :
            label(x), next(NULL), random(NULL) {
    }
};
*/
class Solution {
public:
    RandomListNode* Clone(RandomListNode* pHead)
    {
        if(pHead==nullptr)return nullptr;
        RandomListNode *dummy=new RandomListNode(-1),*cur=dummy;
        unordered_map<RandomListNode*,RandomListNode*>dict;
        auto *t=pHead;
        while(pHead!=nullptr){
            RandomListNode *temp=new RandomListNode(pHead->label);
            dict[pHead]=temp;
            cur->next=temp;
            cur=cur->next;
            pHead=pHead->next;
        }
        cur=dummy->next;
        while(t){
            cur->random=dict[t->random];
            cur=cur->next;
            t=t->next;
        }
        return dummy->next;
    }
};
```

