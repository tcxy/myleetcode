# Single Number

## Description

Given a non-empty array of integers, every element appears twice except for one. Find that single one.

## 思路

这道题最直观的方法就是用一个字典来存储每个数字出现的次数然后返回只出现一次的那个数字。但是题目希望我们尽量不要使用额外的空间，那就需要利用数组本身了。这道题可以利用的就是亦或方法了，因为a xor b = 0/1，但是0异或任何一个数都是其本身，再次异或则变为0。如果数组中只有一个数只出现一次的话，那么数组中所有的数和0异或的结果就是这个数。

## 代码

``` python
class Solution(object):
    def singleNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        res = 0
        for num in nums:
            res ^= num
        return res
```