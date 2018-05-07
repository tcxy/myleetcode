# Implement strStr()

## Description

Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

## 思路

其实就是先判断needle是否为空， 不为空的情况遍历字符串然后看子字符串就行了

## 代码

```
class Solution:
    def strStr(self, haystack, needle):
        """
        :type haystack: str
        :type needle: str
        :rtype: int
        """
        if len(needle) == 0:
            return 0
        for i in range(len(haystack) - len(needle) + 1):
            if haystack[i:i + len(needle)] == needle:
                return i
        return -1
```