# 剑指offer [44. 数字序列中的某一位数字](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=_44-数字序列中的某一位数字)

## [题目描述](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=题目描述-3)

数字以 0123456789101112131415... 的格式序列化到一个字符串中，求这个字符串的第 index 位。

## [解题思路](https://cyc2018.github.io/CS-Notes/#/notes/剑指 Offer 题解 - 40~49?id=解题思路-5)

```cpp
int getDigitIndex(int index) {
	if (index<10)
		return index;
	index -= 10;
	int len = 1;
	while (index>9 * pow(10, len)*(len+1)) {
		index -= 9 * pow(10, len)*(len+1);
		len++;
	}
	int m = index / (len+1), n = index % (len+1);
	int numbers = pow(10, len) + m;
	string res = to_string(numbers);
	return res[n]-'0';
}
```

