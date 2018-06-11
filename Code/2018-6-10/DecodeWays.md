# Decode Ways

## Description

A message containing letters from A-Z is being encoded to numbers using the following mapping:

>
'A' -> 1
'B' -> 2
...
'Z' -> 26

Given a non-empty string containing only digits, determine the total number of ways to decode it.

## 思路

感觉跟求子集那道题基本差不多，但是这里有限制条件，就是最大值只能为26。实际上本题还是一道DP题，当字符串长度为s的时候，主要取决于s-1和s-2能有多少个值。这里需要注意一点判断，因为如果第s个值是'0'的话，那么是不能构成一个单字符的，它只能和前面的值合在一起计算。所以对于非'0'的情况我们需要考虑s-1，然后所有的值都需要考虑s-2

## 代码

``` python
class Solution:
    def numDecodings(self, s):
        """
        :type s: str
        :rtype: int
        """
        if s == '':
            return 0
        dp = [0 for x in range(len(s) + 1)]
        dp[0] = 1
        for i in range(1, len(s) + 1):
            if s[i-1] != '0':
                dp[i] = dp[i-1]
            if i > 1 and s[i-2:i] < '27' and s[i-2:i] > '09':
                dp[i] += dp[i-2]
        return dp[len(s)]
```