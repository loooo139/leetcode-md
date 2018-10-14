# leetcode  17. Letter Combinations of a Phone Number

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![img](http://upload.wikimedia.org/wikipedia/commons/thumb/7/73/Telephone-keypad2.svg/200px-Telephone-keypad2.svg.png)

**Example:**

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**Note:**

Although the above answer is in lexicographical order, your answer could be in any order you want.

## 解题思路

利用递归来求解 我们建立一个字典用来保存每个数字所代表的字母，然后我们还需要设置一个变量level ，记录当前生成的字符串的字符个数

```c++
vector<string> letterCombinations(string digits){
    vector<string> res;
    if(digits.empty())return res;
    string dict[]={"abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
    letterCombinationsDFS(digits,dict,0,"",res);
    return res;
}
void letterCombinationsDFS(string digits,string dict[],int level,string out ,vector<string>&res)
{
    if(level==digits.size())res.push_back(out);
    else{
        string str=dict[digits[level]-'2'];
        for(int i=0;i<str.size();i++){
            out.push_back(str[i]);
            letterCombiantionsDFS(digits,dict,level+1,out,res);
            out.pop_back();
        }
    }
}
```

### 另一个版本

```c++
vector<string> letterCombinations(string digits){
    vector<string>res;
    string charmap[10] = {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    res.push_back("");
    for(int i=0;i<digits.size();i++){
        vector<string>temp;
        int val=digits[i]-'0';
        for(int j=0;j<charmap[val].size();j++){
            for(int k=0;k<res.size();k++){
                temp.push_back(res[k]+charmap[val][j]);
            }
        }
        res=temp;
    }
    return res;
}
```

```pyhton
def letterCombinations(self,digits):
	ans=[''] if digits else []
	for d in figits:
		ans=[res+add for add in digits[d] for res in ans]
	return ans
```

