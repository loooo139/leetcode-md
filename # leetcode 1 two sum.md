# leetcode 1 two sum

* https://leetcode.com/problems/two-sum/

> Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.
>
> You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.
>
> **Example:**
>
> ```
> Given nums = [2, 7, 11, 15], target = 9,
> 
> Because nums[0] + nums[1] = 2 + 7 = 9,
> return [0, 1].
> ```

利用hashmap可以在O(n)的时间复杂度下完成,整体思想是记录数字出现的位置,map<int,int>将数字和其出现的位置映射起来.

```c++
public:
vector<int> twoSum(vector<int> &num,int target){
    unordered_map<int,int>hashtable;
    for(int i=0;i<num.size();i++){
        if(hashtable.cout(target-num[i])){
            return {i,hashtable[target-num[i]};
        }
        else
                    hashtable[num[i]]=i;
    }
                    return{};
}
```
