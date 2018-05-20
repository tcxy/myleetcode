# Pow(x, n)

## Description

Implement pow(x, n), which calculates x raised to the power n(x^x).

## 思路

整体来说，这题不怎么难，pow的实现其实就是乘法而已，但是我尝试的时候超时了。如果要在短时间内完成的话，可能需要考虑利用分治来解决问题。如果使用分治的话，其实有点类似另外创建一个n维数组，然后每个元素都是x再进行分治，但是这样就已经到了O(n)了，应该也会超时。换个思路想的话，如果我改动x和n的值，就可以缩短需要执行的次数，比如2的4次，其实等于4的2次。主要问题就在于什么时候我可以改变x的值，基本上就是n为偶数的时候。这样就可以缩短执行的次数。

## 代码

``` python
class Solution:
    def myPow(self, x, n):
        """
        :type x: float
        :type n: int
        :rtype: float
        """
        sign = -1 if n < 0 else 1
        n = abs(n)
        if abs(x) > 100:
            return
        result = 1
        while n:
            if n % 2 == 0:
                x = x * x
                n //= 2
            else:
                result *= x
                n -= 1
        result = 1 / result if sign == -1 else result
        return min(2**31-1, max(-2**31, result))
```

## 总结

这题主要是要想到x的值也是可以更改的。