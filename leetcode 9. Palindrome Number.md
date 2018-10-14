# leetcode 9. Palindrome Number

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

**Example 1:**

```
Input: 121
Output: true
```

**Example 2:**

> loveyou
>
>

```
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.
```

**Example 3:**

```
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.
```

**Follow up:**

Coud you solve it without converting the integer to a string?

```c
bool isPalindrome(int x){
    int x_=x;
    if(x<0||(x%10==0&&x!=0))return 0;
    int res=0;
    while(x){
        res=res*10+x%10;
        x/=10;
    }
    if(res==x_)return ture;
    else return false;
}
```

