# leetcode 3 zigzag conversion

 The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: `"PAHNAPLSIIGYIR"`

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string s, int numRows);
```

**Example 1:**

```
Input: s = "PAYPALISHIRING", numRows = 3
Output: "PAHNAPLSIIGYIR"
```

**Example 2:**

```
Input: s = "PAYPALISHIRING", numRows = 4
Output: "PINALSIGYAHRPI"
Explanation:

P     I    N
A   L S  I G
Y A   H R
P     I
```

```c++
string convert(string s, int numRows){
    int len=2*numRows-1;
    string res[numRows]={};
    if(numRows<=1)return s;
    int idx=0,step=1;
    for(int i=0;i<s.size();i++){
        res[idx]+=s[i];
        if(idx==numRow-1){
            step=-1;
        }else if(idx==0){
            step=1;
        }
        idx+=step;
    }
    string tmp="";
    for(auto i : res){
        tmp+=i;
    }
    return tmp;
}
```

