# leetcode 31 next-permutation

# [Next Permutation](https://leetcode.com/problems/next-permutation/description/)

|  Category  |   Difficulty    | Likes | Dislikes |
| :--------: | :-------------: | :---: | :------: |
| algorithms | Medium (30.28%) | 1836  |   576    |

<details style="color: rgb(248, 248, 242); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe WPC&quot;, &quot;Segoe UI&quot;, Ubuntu, &quot;Droid Sans&quot;, sans-serif, &quot;Microsoft Yahei UI&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary><strong>Tags</strong></summary></details>

<details style="color: rgb(248, 248, 242); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe WPC&quot;, &quot;Segoe UI&quot;, Ubuntu, &quot;Droid Sans&quot;, sans-serif, &quot;Microsoft Yahei UI&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary><strong>Companies</strong></summary></details>

Implement **next permutation**, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be **in-place** and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

```
1,2,3` → `1,3,2`
`3,2,1` → `1,2,3`
`1,1,5` → `1,5,1
```

比如现在有排列` 1 2 7 4 3 1 `其下一排列时` 1 3 1 2 7 4`。其做法是从后往前找到第一个下降的点，然后找到第一个大于等有这个点的数字该题时3，交换两个位置。` 1 3 7 4 2 1`，然后在该点后面的片段，反转。

```cpp
void next_permutation(vector<int>&nums){
    int i,j,n=nums.size();
    for(i=n-2;i>=0;i--){
        if(nums[i]<nums[i+1]){
            j=n-1;
            while(nums[j]<=nums[i]){
                j--;
            }
            swap(nums[i],nums[j]);
            reverse(nums.begin()+i+1,nums.end());
            return ;
            
        }
    }
    reverse(nums.begin(),nums.end());
}
```

