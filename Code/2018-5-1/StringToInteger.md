# String to Integer (atoi)

## Project description

Implement atoi which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

Note:

Only the space character ' ' is considered as whitespace character.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.

## 思路

基本上思路已经在介绍里面说过了，首先要去除最前面的空格。然后判断+/-号或者字符串是否为空，最后再计算数值。

## 代码

```
class Solution(object):
    def myAtoi(self, str):
        """
        :type str: str
        :rtype: int
        """
        result = 0
        sign = 1
        digits = 0
        i = 0
        if len(str) < 1 or str == "-" or str == "+":
            return 0
        str = self.removeSpace(str)
        if len(str) < 1:
            return 0
        if str[0] == '-':
            str = str[1:]
            sign = -1
        elif str[0] == '+':
            str = str[1:]
        while i < len(str) and str[i].isdigit():
            result *= 10
            result += ord(str[i]) - ord('0')
            i += 1
            digits += 1
        return min(result, 2**31) * sign
        
        
    
    def removeSpace(self, str):
        i = 0
        while i < len(str) and str[i] == ' ':
            i += 1
        return str[i:]
```

## 总结

整体来说这题其实不难，基本是O(n)，所以也没必要太在意。直接遍历然后判断每个字符就行了，我的代码比较麻烦。主要是我比较担心出现几种情况：比如前面后面都存在加号或者减号，又或者中间隔了一段字符之后又出现数字，在一定程度上，我觉得用一个循环可能会更加麻烦。这题目最容易忽略的情况就是空字符串或者全部都是由空格组成的字符串，思考的时候要注意。

## 其他人的方案

```
class Solution(object):
    def myAtoi(self, s):
        """
        :type str: str
        :rtype: int
        """
        ###better to do strip before sanity check (although 8ms slower):
        #ls = list(s.strip())
        #if len(ls) == 0 : return 0
        if len(s) == 0 : return 0
        ls = list(s.strip())
        
        sign = -1 if ls[0] == '-' else 1
        if ls[0] in ['-','+'] : del ls[0]
        ret, i = 0, 0
        while i < len(ls) and ls[i].isdigit() :
            ret = ret*10 + ord(ls[i]) - ord('0')
            i += 1
        return max(-2**31, min(sign * ret,2**31-1))
```

这个方案应该是目前最好的，除了ls创建之后还要判断一下是否为空。