# leetcode 34.[Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

|  Category  |   Difficulty    | Likes | Dislikes |
| :--------: | :-------------: | :---: | :------: |
| algorithms | Medium (33.30%) | 1656  |    89    |

<details style="color: rgb(248, 248, 242); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe WPC&quot;, &quot;Segoe UI&quot;, Ubuntu, &quot;Droid Sans&quot;, sans-serif, &quot;Microsoft Yahei UI&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary><strong>Tags</strong></summary></details>

<details style="color: rgb(248, 248, 242); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe WPC&quot;, &quot;Segoe UI&quot;, Ubuntu, &quot;Droid Sans&quot;, sans-serif, &quot;Microsoft Yahei UI&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary><strong>Companies</strong></summary></details>

Given an array of integers `nums` sorted in ascending order, find the starting and ending position of a given `target` value.

Your algorithm's runtime complexity must be in the order of *O*(log *n*).

If the target is not found in the array, return `[-1, -1]`.

**Example 1:**

```
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]
```

**Example 2:**

```
Input: nums = [5,7,7,8,8,10], target = 6
Output: [-1,-1]
```

可以使用二分查找的方法找到目标点然后左右扩充。

```cpp
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int n=nums.size(),left=0,right=n-1;
        while(left<=right){
            int mid=left+(right-left)/2;
            if(nums[mid]==target){
                left=mid;
                right=mid;
                break;
            }
            if(nums[mid]<target)
                left=mid+1;
            else
                right=mid-1;
            
        }
        if(left>right)
            return vector<int>{-1,-1};
        while(left>=0&&nums[left]==target)left--;
        while(right<n&&nums[right]==target)right++;
        return vector<int>{left+1,right-1};
    }
};
```

