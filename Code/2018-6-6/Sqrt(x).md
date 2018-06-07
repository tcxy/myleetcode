# Sqrt(x)

## Description

Implement int sqrt(int x).

Compute and return the square root of x, where x is guaranteed to be a non-negative integer.

Since the return type is an integer, the decimal digits are truncated and only the integer part of the result is returned.

## 思路

这题实在没什么思路，之后搜了一下，可以用二分来解决。当然由于这个问题要求返回整数，所以在一定程度上反而更麻烦。我试了几个方案，都是直接超时。

## 代码

``` python
class Solution:
    def mySqrt(self, x):
        """
        :type x: int
        :rtype: int
        """
        ans = 0
        bit = 1 << 15
        while bit > 0:
            ans |= bit
            if ans * ans > x:
                ans ^= bit
            bit >>= 1
        return int(ans)
```

## 总结

感觉很玄学，还是直接背答案吧。