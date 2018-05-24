# Wildcard Matching

## Description

Given an input string (s) and a pattern (p), implement wildcard pattern matching with support for '?' and '*'.

## 思路

其实跟Regular Expression Match那道题基本一样，只是？和.的区别。按照那道题的思路，可以利用动态规划来进行。按照个人的想法，那道题其实应该只需要两个数组就够了，一个是current，一个是last，最后从last中进行返回。这道题我看了一种新的解法，之前采用数组的目的就是为了匹配\*，实际上对于\*的匹配也可以按照三种情况来对待：空，单字符，多字符。关键问题是什么时候该停下来，尤其是\*a和aaa这种字符串。新的思路采用的是通过某个变量来记录\*的位置，比如用star来记录。当字符不匹配的时候，可以通过star的位置将p的值回溯过去，同时把s的位置也进行回溯，这样就可以进行多次比对。

## 代码

``` python
class Solution:
    def isMatch(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        s_cur = 0
        p_cur = 0
        star = -1
        match = 0
        
        while s_cur < len(s):
            if p_cur < len(p) and (s[s_cur] == p[p_cur] or p[p_cur] == '?'):
                s_cur += 1
                p_cur += 1
            elif p_cur < len(p) and p[p_cur] == '*':
                match = s_cur
                star = p_cur
                p_cur += 1
            elif star != -1:
                match += 1
                s_cur = match
                p_cur = star
            else:
                return False
        while p_cur < len(p) and p[p_cur] == '*':
            p_cur += 1
        return p_cur == len(p)
```

## 总结

这道题基本上是给了我完全不同的解法，实际上一开始我也倾向于这种解法。但是回溯的条件写的不够好，从另一种角度来看，动态规划其实也是一种需要回溯的算法，但是使用动态规划的时候更重要的是子结构是否存在重叠。尽管如此，子结构重叠了也不见得动态规划就更好。所以在做题的时候还是要更加注意分析。