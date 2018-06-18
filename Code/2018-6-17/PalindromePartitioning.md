# Palindrome Partitioning

## Description

Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

## 思路

这题不太清楚，参考之后发现主要是用dfs来进行递归。

## 代码

``` python
class Solution(object):
    def partition(self, s):
        """
        :type s: str
        :rtype: List[List[str]]
        """
        res = []
        self.dfs(s, [], res)
        return res

    def dfs(self, s, path, res):
        if not s:
            res.append(path)
            return
        for i in range(1, len(s)+1):
            if s[:i] == s[:i][::-1]:
                self.dfs(s[i:], path+[s[:i]], res)
```