# 剑指offer 43 从1到n整数中1出现的次数

```cpp
int countNumberOfOne(int n){
    int res=0;
    for(int i=1;i<=n;i*=10){
        int a=n/i,b=n%i;
        if(a%10==0)
            res+=a/10*i;
        if(a%10==1)
            res+=a/10*i+b+1;
        if(a%10>=2)
            res+=a/10*i+i;
        // res+=(a+8)/10*i+(a%10==1?b+1:0);
        
    }
    return res;
}
```

