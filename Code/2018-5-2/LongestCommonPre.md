# Longest Common Prefix

## Description

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

## 思路

这个题目主要是给出的参数是包含string的一个list，然后对每个string又要查看当前的char是否相等。麻烦之处在于循环怎么写，思路上倒是不难，如果没有时间限制的话。我觉得直接找出最短的那个字符串对比就行了。

## 代码

```
class Solution:
    def longestCommonPrefix(self, strs):
        """
        :type strs: List[str]
        :rtype: str
        """
        if not strs:
            return ""
        shortest = min(strs,key=len)
        for i, char in enumerate(shortest):
            for str in strs:
                if str[i] != char:
                    return shortest[:i]
        return shortest
```