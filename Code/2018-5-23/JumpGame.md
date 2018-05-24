# Jump Game

## Description

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

## 思路

主要是步数能够到最后就行了，开始的步数为nums[0]。每走一步减一，同时与新的值比较，最后看能不能到。

## 代码

``` python
class Solution:
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        stepsLeft = nums[0]

        if not stepsLeft and len(nums) > 1:
            return False

        for num in nums[1:-1]:
            stepsLeft = max(stepsLeft - 1, num)
            if not stepsLeft:
                return False

        return True
```