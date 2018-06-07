# Plus One

## Description

Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

## 思路

这题非常简单，说白了就是倒着遍历一遍就可以了。当然，也可以更省时间一点，比如我确认add位之后，只要add为0就终止。

## 代码

``` python
class Solution:
    def plusOne(self, digits):
        """
        :type digits: List[int]
        :rtype: List[int]
        """
        lend = len(digits)
        digits[lend-1] += 1
        add = 0
        for i in range(lend-1, -1, -1):
            digits[i] += add
            if digits[i] == 10:
                digits[i] = 0
                add = 1
            else:
                add = 0
                break
        if add == 1:
            digits.insert(0, add)
        return digits
```