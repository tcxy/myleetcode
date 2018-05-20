# Maximum Subarray

## Description

Given an integer array nums, find the contiguous subarray which has the largest sum and return its sum

## 思路

基本上直接过一遍就行了，然后当前面值相加还不如当前值大的时候更新当前值。

## 代码

``` python 
class Solution:
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0

        curSum = maxSum = nums[0]
        for num in nums[1:]:
            curSum = max(num, curSum + num)
            maxSum = max(maxSum, curSum)

        return maxSum
```