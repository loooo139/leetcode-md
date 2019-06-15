# 剑指offer [30. 包含 min 函数的栈](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=_30-包含-min-函数的栈)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述)

定义栈的数据结构，请在该类型中实现一个能够得到栈[最小元素](http://www.baidu.com)的 min 函数。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=解题思路)

> 定义一个栈的数据结构，实现可以获取栈中最小的元素的操纵，要求 min、push、pop的时间复杂度都是常数。

```cpp
class Solution{
    private:
    stack<int>st1,st2;
    public:
    void push(int val){
        if(st1.empty()){
            st2.push(val);
        }
        else{
            int temp=st2.top();
            st2.push(min(temp,val));
        }
        st1.push(val);
        
    }
    int top(){
        return st1.top();
    }
    void min(){
        return st2.top();
    }
    void pop(){
        st1.pop();
        st2.pop();
    }
}
```

