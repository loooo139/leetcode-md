# [剑指offer 9. 用两个栈实现队列](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 3~9?id=_9-用两个栈实现队列)

[NowCoder](https://www.nowcoder.com/practice/54275ddae22f475981afa2244dd448c6?tpId=13&tqId=11158&tPage=1&rp=1&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 3~9?id=题目描述-6)

用两个栈来实现一个队列，完成队列的 Push 和 Pop 操作。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 3~9?id=解题思路-6)

in 栈用来处理入栈（push）操作，out 栈用来处理出栈（pop）操作。一个元素进入 in 栈之后，出栈的顺序被反转。当元素要出栈时，需要先进入 out 栈，此时元素出栈顺序再一次被反转，因此出栈顺序就和最开始入栈顺序是相同的，先进入的元素先退出，这就是队列的顺序。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/3ea280b5-be7d-471b-ac76-ff020384357c.gif)

```cpp
class Solution{
    public:
    void push(int val){
        st1.push(val);
    }
    int pop(){
        if(st2.empty()){
            while(!st1.empty()){
                st2.push(st1.top());
                st1.pop();
            }
        }
        if(st2.empty())return -1;
        else{
            int t=st2.top();
            st2.pop();
            return t;
        }
    }
private:
    stack<int>st1,st2;
}
```

