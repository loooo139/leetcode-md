# 剑指offer 替换空格

---

>
>
>**c/c++ 中每个字符串都规定以字符‘/0’结尾，这样可以方便的找到字符串的结尾。但是同样由于这个问题，字符串存在额外的开销**
>
>另外，为了节省内存，**c/c++中把常量字符串放到一个单独的内存区域 **。当几个指针赋值给相同的常量字符串的时候，他们实际上会指向相同的内存地址。但用常量内存去初始化数组，情况却有所不同。
>
>

将一个字符串中的空格替换成 "%20"。

```text
Input:
"A B"

Output:
"A%20B"
```

## 解题思路

若题目要求可以新建字符串，则可以新建字符串进行解决。若不允许新建字符串，则原字符串需要有足够长的空间来容纳新字符串。应该先先计算出新字符串的末尾长度，扫描一遍源字符串，计算得出新字符串的长度。然后双指针，一个指向原来的结尾，一个指向新的结尾。从后往前遍历原来的字符串，遇到非空字符则复制前移，遇到为空则复制%20.直到尽头。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/6980aef0-debe-4b4b-8da5-8b1befbc1408.gif)

```cpp
void repalceBlank(char string[],int length){
    if(string==nullptr||length<=0)
        return;
    int numOfBlank=0;
    int i=0;
    while(string[i]!=0){
        if(string[i]==' ')
            numOfBlank++;
        i++;
    }
    int j=i+2*numOfBlank;
    if(j>length)return ;
    while(i>=0&&j>=0){
        if(string[i]!=' '){
            string[j--]=string[i--];
        }
        else{
            string[j--]='0';
            string[j--]='2';
            string[j--]='%';
            i--;
        }
    }
    
}
```

