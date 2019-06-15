# 剑指offer  [11. 旋转数组的最小数字](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 10~19?id=_11-旋转数组的最小数字)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 10~19?id=题目描述-4)

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/0038204c-4b8a-42a5-921d-080f6674f989.png)

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 10~19?id=解题思路-4)

将旋转数组对半分可以得到一个包含最小元素的新旋转数组，以及一个非递减排序的数组。新的旋转数组的数组元素是原数组的一半，从而将问题规模减少了一半，这种折半性质的算法的时间复杂度为 O(logN)（为了方便，这里将 log2N 写为 logN）。

![img](https://cs-notes-1256109796.cos.ap-guangzhou.myqcloud.com/424f34ab-a9fd-49a6-9969-d76b42251365.png)

此时问题的关键在于确定对半分得到的两个数组哪一个是旋转数组，哪一个是非递减数组。我们很容易知道非递减数组的第一个元素一定小于等于最后一个元素。

通过修改二分查找算法进行求解（l 代表 low，m 代表 mid，h 代表 high）：

- 当 nums[m] <= nums[h] 时，表示 [m, h] 区间内的数组是非递减数组，[l, m] 区间内的数组是旋转数组，此时令 h = m；
- 否则 [m + 1, h] 区间内的数组是旋转数组，令 l = m + 1。

```cpp
class Solution {
public:
    int minNumberInRotateArray(vector<int> rotateArray) {
        if(rotateArray.empty())return 0;
        int left=0,right=rotateArray.size()-1;
        if(rotateArray[0]<rotateArray[right])return rotateArray[0];
        while(left<right){
            if(left==right-1) return rotateArray[right];
            int mid=(left+right)/2;
            if(rotateArray[mid]<=rotateArray[right])
                right=mid;
            else
                left=mid+1;
        }
        return 0;
    }
};
```

