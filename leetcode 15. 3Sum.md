# leetcode 15. 3Sum

Given an array `nums` of *n* integers, are there elements *a*, *b*, *c* in `nums` such that *a* + *b* + *c* = 0? Find all unique triplets in the array which gives the sum of zero.

**Note:**

The solution set must not contain duplicate triplets.

**Example:**

```
Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

------



 ## 解题思路

思路和two sum类似都是查找指定的数字之和，只是现在是三个数字，首先将数组排序，然后从左到右依次查找；

```c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        sort(nums.begin(),nums.end());
        vector<vector<int>>res;
        for(int i=0;i<nums.size();i++){
            if(i&&nums[i]==nums[i-1]) continue;
            if(nums[i]>0) return res;
            int j=i+1,k=nums.size()-1;
            while(j<k){
                if(nums[j]+nums[k]==-nums[i]){
                    res.push_back({nums[i],nums[j],nums[k]});
                    while(nums[j]==nums[j+1]) j++;
                    while(nums[k]==nums[k-1])k--;
                    j++;k--;
                }
                else if(nums[j]+nums[k]<-nums[i]) j++;
                else k--;
            }
        }
        return res;
    }
};
```



``` c++
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        if (!nums.empty() && nums.back() < 0) return {};
        for (int k = 0; k < nums.size(); ++k) {
            if (nums[k] > 0) break;
            if (k > 0 && nums[k] == nums[k - 1]) continue;
            int target = 0 - nums[k];
            int i = k + 1, j = nums.size() - 1;
            while (i < j) {
                if (nums[i] + nums[j] == target) {
                    res.push_back({nums[k], nums[i], nums[j]});
                    while (nums[i] == nums[i + 1]) ++i;
                    while (nums[j] == nums[j - 1]) --j;
                    ++i; --j;
                } else if (nums[i] + nums[j] < target) ++i;
                else --j;
            }
        }
        return res;
    }
};
```



