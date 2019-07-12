# leetcode 40.[Combination Sum II](https://leetcode.com/problems/combination-sum-ii/description/)

|  Category  |   Difficulty    | Likes | Dislikes |
| :--------: | :-------------: | :---: | :------: |
| algorithms | Medium (40.95%) |  869  |    47    |

<details style="color: rgb(248, 248, 242); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe WPC&quot;, &quot;Segoe UI&quot;, Ubuntu, &quot;Droid Sans&quot;, sans-serif, &quot;Microsoft Yahei UI&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary><strong>Tags</strong></summary></details>

<details style="color: rgb(248, 248, 242); font-family: -apple-system, BlinkMacSystemFont, &quot;Segoe WPC&quot;, &quot;Segoe UI&quot;, Ubuntu, &quot;Droid Sans&quot;, sans-serif, &quot;Microsoft Yahei UI&quot;; font-size: 16px; font-style: normal; font-variant-ligatures: normal; font-variant-caps: normal; font-weight: 400; letter-spacing: normal; orphans: 2; text-align: start; text-indent: 0px; text-transform: none; white-space: normal; widows: 2; word-spacing: 0px; -webkit-text-stroke-width: 0px; text-decoration-style: initial; text-decoration-color: initial;"><summary><strong>Companies</strong></summary></details>

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sums to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:**

- All numbers (including `target`) will be positive integers.
- The solution set must not contain duplicate combinations.

**Example 1:**

```
Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**Example 2:**

```
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```

还是标准的dfs，permutation的做法。与上体不同的需要加入去重

```cpp
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
                vector<vector<int>>res;
        vector<int>tmp;
        sort(candidates.begin(),candidates.end());
        if(target<candidates[0])return res;
        vector<bool>flag(candidates.size(),false);
        DFS(res,tmp,candidates,target,0,flag);
        return res;
    }
        void DFS(vector<vector<int>>&res,vector<int>&tmp,vector<int>candi,int target,int index,vector<bool>&flag){
        if(target==0){
            res.push_back(tmp);
            return ;
        }
        if(target<0) return ;
        for(int i=index;i<candi.size();i++){
            if(candi[i]<=target){
                if(i!=index&&candi[i]==candi[i-1]&&flag[i-1]==false) continue;
                tmp.push_back(candi[i]);
                flag[i]=true;
                DFS(res,tmp,candi,target-candi[i],i+1,flag);
                flag[i]=false;
                tmp.pop_back();
            }
        }
        
    }
};


```

