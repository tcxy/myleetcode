# Subsets

## Description

Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

## 思路

这道题感觉也是属于动态规划的一道题，实际上可构成的数组，从长度为0一直到n。然后每一个数组都是在之前的基础上完成的，这个题目有点像之前的括号匹配还有电话号码的一道题。

## 代码

``` python
class Solution:
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = [[]]
        for num in nums:
            res += [item + [num] for item in res]
        return res
```

## 总结

这道题的思路其实之前也出现过很多次，有必要做一个专题。