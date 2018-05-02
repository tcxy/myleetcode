# Reverse Integer

## Description

Given a 32-bit signed integer, reverse digits of an integer.

## 思路

这题非常简单，一边遍历一边算结果就可以了。每次可以去最后一位，这一位正好加到新的数字上，然后把新数字乘以10即可。需要注意的是，输入值的符号需要进行判断。

## 代码

```
class Solution(object):
    def reverse(self, x):
        """
        :type x: int
        :rtype: int
        """
        sign = 1
        result = 0
        if x < 0:
            sign = -1
            x = abs(x)
        while x > 0:
            result = result * 10 + x % 10
            x = x // 10
        return result * sign
```