# leetcode 16. 3Sum Closest

------

Given an array `nums` of *n* integers and an integer `target`, find three integers in `nums` such that the sum is closest to `target`. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example:**

```
Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

```c++
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {
        sort(nums.begin(),nums.end());
        int sum=nums[0]+nums[1]+nums[nums.size()-1];
        int dif=abs(sum-target);
        for(int i=0;i<nums.size();i++){
            int j=i+1,k=nums.size()-1;
            while(j<k){
                if(abs(nums[i]+nums[j]+nums[k]-target)<dif){
                    dif=abs(nums[i]+nums[j]+nums[k]-target);
                    sum=nums[i]+nums[j]+nums[k];
                }
                if(nums[i]+nums[j]+nums[k]<target) j++;
                else k--;
            }
        }
        return sum;
    }
};
```

