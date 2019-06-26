# leetcode 29 [Divide Two Integers](https://leetcode.com/problems/divide-two-integers/description/)

|  Category  |   Difficulty    | Likes | Dislikes |
| :--------: | :-------------: | :---: | :------: |
| algorithms | Medium (16.15%) |  693  |   3282   |



Return the quotient after dividing `dividend` by `divisor`.

The integer division should truncate toward zero.

**Example 1:**

```
Input: dividend = 10, divisor = 3
Output: 3
```

**Example 2:**

```
Input: dividend = 7, divisor = -3
Output: -2
```

**Note:**

- Both dividend and divisor will be 32-bit signed integers.
- The divisor will never be 0.
- Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 231 − 1 when the division result overflows.

利用位运算来计算，首先用long 类型保存除数m，被除数 n，在循环里面定义变量t等于n、计数p为，若m>t的2倍，则 t，p变为二倍，否则跳出循环，res+=p,m-=t;

```cpp
int divide(int dividend,int divisor){
    long long m=abs(long long dividend),n=abs(long long divisor),res=0;
    if(m<n)return 0;
    while(m>=n){
        long long t=n,p=1;
        while(m>(t<<1)){
            t<<=1;
            p<<=1;
        }
        res+=p;
        m-=t;
    }
    if((dividend<0)^(divisor<0))res=-res;
    return rse>INT_MAX?INT_MAX:res;
}
```

