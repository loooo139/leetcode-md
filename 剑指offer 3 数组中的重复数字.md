# 剑指offer 3 数组中的重复数字

> 在一个长度为n的数组中，所有重复的数字范围都在0-n-1中，数组中某些数字是重复但是不知道哪些数字是重复的，请找出数组中任意一个重复的数字。

如果没有重复数字那么数字i应该排列在位置i上，既然存在重复的数字。那么有些位置上数字会重复出现。我们从头到尾扫描这个数组，对于位置i的数字j，查看i，j是否相等若不相等，则交换位置i，j上的数字，若位置i,j上的数字相等，则找到重复数字。重复直至相等。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/49d2adc1-b28a-44bf-babb-d44993f4a2e3.gif)

```cpp
class Solution {
public:
    // Parameters:
    //        numbers:     an array of integers
    //        length:      the length of array numbers
    //        duplication: (Output) the duplicated number in the array number
    // Return value:       true if the input is valid, and there are some duplications in the array number
    //                     otherwise false
    bool duplicate(int numbers[], int length, int* duplication) {
        bool flag=false;
        for(int i=0;i<length;i++){
            while(numbers[i]!=i){
                if(numbers[i]!=numbers[numbers[i]]){
                    swap(numbers[i],numbers[numbers[i]]);
                }
                else{
                    *duplication=numbers[i];
                    return true;
                }
            }
        }
        return flag;
    }
};
```

## 变种 -不修改原来的数组

现在题目要求改为不能修改原数组。比较简单的新建一个n+1长度的数组往里面填数字就可以了。

不使用额外的空间解法是，类似二分查找。统计区间里面的数字个数。我们把1-n的数字分为1-m，m+1-n。若1-m数字中不存在重复的数字则一共有m个数字。若存在重复的数字则个数大与m。不断二分进行查找。

```cpp
int getDuplication(const int * nunmbers,int length){
    int start=1,end=length-1;
    while(end>=start){
        int middle=(end-start)>>1+start;
        int count=countRange(numbers,length,start,end);
        if(end==start){
            if(count>1)
                return start;
            else
                break;
        }
        if(count>(middle-start+1))
            end=middle;
        else
            start=middle+1;
    }
    return -1;
}
int countRange(const int* numbers,int length,int start,int end){
    int count=0;
    for(int i=0;i<lenght;i++)
        if(numbers[i]>=start&&numbers[i]<=end)
            count++;
    return count;
}
```

