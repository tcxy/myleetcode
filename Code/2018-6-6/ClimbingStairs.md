# Climbing Stairs

## Description

You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

## 思路

还是最基本的DP

## 代码

``` python
class Solution:
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        res = [0] * n
        res[0] = 1
        if n == 1:
            return 1
        res[1] = 2
        for i in range(2, n):
            res[i] = res[i-1] + res[i-2]
        return res[n-1]
```

## 总结

差点翻船，这题要注意如果n为1怎么办。