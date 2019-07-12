# leetcode 42.[Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/)

|  Category  |  Difficulty   | Likes | Dislikes |
| :--------: | :-----------: | :---: | :------: |
| algorithms | Hard (42.65%) | 3767  |    70    |

<details style="color: rgb(248, 248, 242); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe WPC&quot;, &quot;Segoe UI&quot;, Ubuntu, &quot;Droid Sans&quot;, sans-serif, &quot;Microsoft Yahei UI&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary><strong>Tags</strong></summary></details>

<details style="color: rgb(248, 248, 242); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe WPC&quot;, &quot;Segoe UI&quot;, Ubuntu, &quot;Droid Sans&quot;, sans-serif, &quot;Microsoft Yahei UI&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary><strong>Companies</strong></summary></details>

Given *n* non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![img](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)
The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image!

**Example:**

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

本题目有两种方法最简单的就是两边扫描。从左扫一遍记录下最大的值，在从右扫一遍然后找最大值取最大值的较小值即可。

```cpp
public:
    int trap(vector<int>& height) {
        int n=height.size();
        vector<int>m_height(height.begin(),height.end());
        int maxHeight=INT_MIN;
        for(int i=1;i<n;i++){
            maxHeight=max(height[i-1],maxHeight);
            m_height[i]=maxHeight;
        }
        int res=0;
        maxHeight=INT_MIN;
        for(int i=n-2;i>=0;i--){
            maxHeight=max(height[i+1],maxHeight);
            m_height[i]=min(maxHeight,m_height[i]);
            if(m_height[i]>height[i])
                res+=m_height[i]-height[i];
        }
        return res;
    }
};
```

第二种方法是一边扫描双指针的做法。

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int l=0,n=height.size(),r=n-1;
        int res=0;
        while(l<r){
            int min_h=min(height[l],height[r]);
            if(min_h==height[l]){
                l++;
                while(l<r&&height[l]<min_h){
                    res+=min_h-height[l++];
                }
            }
            else{
                r--;
                while(l<r&&height[r]<min_h){
                    res+=min_h-height[r--];
                }
            }
        }
        return res;
    }
};
```

