# Search for a range

## Description

Given an array of integers nums sorted in ascending order, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

## 思路

感觉还是二分查找，这里主要是要找出所有的相等的数字。基本思路还是绕不开left，right和mid这三个数字。因为要找出来的是所有的相等的数字，所以重点在于当mid和target相等之后的条件要怎么判断。比如，target这个数字最早正好在left和mid之间，而最迟正好出现在right和mid之间。这个时候需要做的事情就是，找到一个数正好等target，使其左边小于这个数。

## 代码

```
class Solution:
    def searchRange(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        left = 0
        right = len(nums) - 1
        start = -1
        end = -1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                start = self.findStart(nums, left, mid, target)
                end = self.findEnd(nums, mid, right, target)
                return [start, end]
            elif nums[mid] > target:
                right = mid - 1
            elif nums[mid] < target:
                left = mid + 1
        return [-1, -1]

    def findStart(self, nums, left, right, target):
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                if mid == 0 or nums[mid - 1] != target:
                    return mid
                else:
                    right = mid - 1
            elif nums[mid] < target:
                left = mid + 1
        return -1

    def findEnd(self, nums, left, right, target):
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                if mid == len(nums) - 1 or nums[mid + 1] != target:
                    return mid
                else:
                    left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
        return -1
```

## 总结

看了一下别人的思路，要么是通过二分查找找到相等的一个数，然后直接用循环的形式来找到start和end。要么是通过找到target之后通过加减来找target两边的数来计算。个人认为这两种算法应该是不符合要求的，原因是这样的，对于第一种算法来说，算法的时间复杂度完全取决于数组的特性。比如，我取一个[8,8,8,8,8,8]然后target设置为8，那么这个算法的实际复杂度是O(N)而不是O(log N)。对于第二种来说，漏洞也比较明显，因为我看到的算法里面是直接按照+1和-1来界定大和小。这就形成了一个问题，也就是如果我有一个数组[1,2,3,5,5,5,7,8,9]和target 5，那么在寻找的时候，数组中并不存在4和6，也就出现了返回]-1,-1]的问题。我个人的算法未必是最好的，但是这个算法不管在什么情况下都保证了O(log n)。