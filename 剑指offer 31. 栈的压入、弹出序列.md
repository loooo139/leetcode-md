# 剑指offer [31. 栈的压入、弹出序列](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=_31-栈的压入、弹出序列)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 30~39?id=题目描述-1)

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。

例如序列 1,2,3,4,5 是某栈的压入顺序，序列 4,5,3,2,1 是该压栈序列对应的一个弹出序列，但 4,3,5,1,2 就不可能是该压栈序列的弹出序列。

# 解题思路

----

模拟栈的入栈和出栈，若能成功模拟则成功。

```cpp
bool judge(vector<int>in,vector<int>out){
    if(in.size()!=out.size())return false;
    stack<int>st;
    int i=0,j=0,n=in.size();
    while(i<=n&&j<n){
        while(st.empty()||st.top()!=out[j]){
            if(i==n)return false;
            st.push(in[i++]);
        }
        if(st.top()==out[j]){
            st.pop();
            j++;
        }
    }
    return st.empty();
}
```

```cpp
class Solution {
public:
    bool IsPopOrder(vector<int> pushV,vector<int> popV) {
        stack<int>st;
        int n=pushV.size(),m=popV.size();
        if(n!=m)return false;
        int i=0,j=0;
        while(i<=n&&j<m){
            if(!st.empty()&&st.top()==popV[j]){
                st.pop();
                j++;
            }else{
            while(popV[j]!=pushV[i]){
                st.push(pushV[i++]);
            }
            st.push(pushV[i++]);
            st.pop();j++;
            }
        }
        return st.empty();
    }
};
```

