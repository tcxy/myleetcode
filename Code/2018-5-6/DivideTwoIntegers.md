# Divide Two Integers

## Description

Given two integers dividend and divisor, divide two integers without using multiplication, division and mod operator.

Return the quotient after dividing dividend by divisor.

The integer division should truncate toward zero.

## 思路

感觉就是化为减法来进行计算，注意一下符号和边界就行了。实际算的时候还是超时了，之后想了很久也没有想到合适的方案。看了一下别人的做法感觉思路真的是相当灵活了。

## 代码

```
class Solution:
    def divide(self, dividend, divisor):
        positive = (dividend < 0) is (divisor < 0)
        dividend, divisor = abs(dividend), abs(divisor)
        res = 0
        while dividend >= divisor:
            temp, i = divisor, 1
            while dividend >= temp:
                dividend -= temp
                res += i
                i <<= 1
                temp <<= 1
        if not positive:
            res = -res
        return min(max(-2**31, res), 2**31-1)
```

## 总结

虽然不能用乘法，但是还是可以通过位移来打到乘法的目的。