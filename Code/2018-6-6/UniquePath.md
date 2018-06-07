# Unique Paths

## Description

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

## 思路

一开始看到这道题的时候我是拒绝的，因为这一看就是个DP，是我的弱项。不过仔细分析了一下之后居然一遍过了，思路主要是这样的。对于这样一个棋盘，实际上某一格能够有几种走法，是由这个格子的前一个有多少种走法和这个各自上面的格子有几种走法决定的。由此就构成了DP中的方程，当然我考虑到空间占用的问题，直接用了两个数组来走。这两个数组，一个存放上次的结果，一个存放当前的结果。当执行完了之后，取当前数组的n-1位置的值就可以了。

## 代码

``` python
class Solution:
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        current = [0] * n
        current[0] = 1
        last = current
        while m > 0:
            current = [0] * n
            current[0] = last[0]
            for i in range(1, n):
                current[i] = current[i - 1] + last[i]
            last = current
            m -= 1
        return current[n-1]
```

## 总结

算是学习DP之后的一大成果，这题其实是非常简单的DP，公式非常好推导。这题也可以算是最适合DP练习的题目了。