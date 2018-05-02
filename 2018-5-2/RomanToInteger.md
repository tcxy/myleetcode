# Roman To Integer

## Description

Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

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

For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

    I can be placed before V (5) and X (10) to make 4 and 9. 
    X can be placed before L (50) and C (100) to make 40 and 90. 
    C can be placed before D (500) and M (1000) to make 400 and 900.

Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

## 思路

这题太简单了，基本就是一个字典然后遍历字符串加到结果就行了。需要注意的就是存在加和减的问题，比如I，X，C这三个值。基本上加完之后减两个就行。按照题目描述连Input的值的边界都不用判断，直接写就行了。

## 代码

```
class Solution:
    def romanToInt(self, s):
        """
        :type s: str
        :rtype: int
        """
        dic = {'I': 1, 'V': 5, 'X': 10, 'L': 50, 'C': 100, 'D': 500, 'M': 1000}
        result = dic[s[0]]
        for i in range(1, len(s)):
            result += -2 * dic[s[i - 1]] + dic[s[i]] if dic[s[i - 1]] < dic[s[i]] else dic[s[i]]
        return result
```

## 总结

这题比较容易遗漏的东西就是I，V，X这些数字在前的情况，有字典的情况下可以直接进行值的比对，当前值是一定要加的，问题在于是不是需要减。直接根据字典中的值来判断就行了。