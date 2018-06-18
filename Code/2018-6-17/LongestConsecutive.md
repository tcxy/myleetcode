# Longest Consecutive Sequence

## Description

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(n) complexity.

## 思路

这题让我想起了之前的一种解法，那就直接按照相应的大小来放置数组中的数，然后再根据排序之后的数组来判断。这样的问题就在于如果连续最大值是在数组长度外的时候怎么办，这样的话，在排序的时候就要开始记录。但是运行之后发现并不太行，因为要排序的话比较难以保证O(n)。

## 代码

``` python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        d = {}
        for num in nums:
            d[num] = True
        longest = 0
        for num in nums:
            length = 1
            temp = num + 1
            while temp in d:
                d.pop(temp)
                length += 1
                temp += 1
            temp = num - 1
            while temp in d:
                d.pop(temp)
                length += 1
                temp -= 1
            longest = max(longest, length)
        return longest
```