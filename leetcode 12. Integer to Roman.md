# leetcode 12. Integer to Roman

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```

For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

- `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
- `X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
- `C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.

Given an integer, convert it to a roman numeral. Input is guaranteed to be within the range from 1 to 3999.

**Example 1:**

```
Input: 3
Output: "III"
```

**Example 2:**

```
Input: 4
Output: "IV"
```

**Example 3:**

```
Input: 9
Output: "IX"
```

**Example 4:**

```
Input: 58
Output: "LVIII"
Explanation: C = 100, L = 50, XXX = 30 and III = 3.
```

**Example 5:**

```
Input: 1994
Output: "MCMXCIV"
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

## 解题思路

1. 本题限制了最大数字在3999因此又有很多的方法去做，最简单的就是提取千，百，十，个的数字然后拼接。

   ```c++
   string intToString(int num){
       string num_k[]={"M","MM","MMM"};
       string num_h[]={"C","CC","CCC","CD","D","DC","DCC","DCCC","CM"};
       string num_t[]={"X","XX","XXX","XL","L","LX","LXX","LXXX","XC"};
       string num_n[]={"I","II","III","IV","V","VI","VII","VIII","IX"};
       return num_k[num/1000]+num_h[num%1000/100]+num_t[num%100/10]+num_n[num%10];
   }
   ```


2. 第二种思路就是不断减去当前的最大值。

   ```C++
   string intToString(int num){
       string str[]={"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};
       int nums[]={1000,900,500,400,100,90,50,40,10,9,5,4,1};
       string res="";
       for(int i=0;i<str.size();i++){
           while(num>=nums[i]){
               res+=str[i];
               num-=nums[i];
           }
       }
       return res;
   }
   ```
