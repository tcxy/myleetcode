# Search in Rotated Sorted Array

## Description

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,1,2,4,5,6,7] might become [4,5,6,7,0,1,2]).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.

Your algorithm's runtime complexity must be in the order of O(log n).

## 思路

要求复杂度为O(log n)，换句话说就是二分查找的变形了。这里的问题在于数组有被动过，不是完全顺序的。所以这题可能还是需要判断一下具体的点才行，基本上还是用low和high来进行比对。但是当mid和target不相等的时候，需要判断一下。以前的时候是mid小于target直接改left，但是现在情况不一样，有可能left到mid就是相应区间。所以如果left < target < mid，就在这个区间进行二分查找。如果不构成这个条件，那有几种情况。比如left和mid中间有个点，正好是转折的点，但是这样情况判断就会变得更复杂了。所以直接先用left，mid，和right来进行判断，这样的话，只要left < mid，要么这个区间是连续的，要么有个点在这中间，如果这时候target正好在这之间，那么直接在这个区间内部寻找。如果target不在这个区间内部，那就不可能在这个区间内部了。当left>mid的时候，可以肯定从left到mid中间一定还存在一个区间，换句话说右边肯定存在一个区间。这样直接在右边区间内部查找就好了。

## 代码

class Solution:
    def search(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        if not nums:
            return -1

        low, high = 0, len(nums) - 1

        while low <= high:
            mid = (low + high) // 2
            if target == nums[mid]:
                return mid

            if nums[low] <= nums[mid]:
                if nums[low] <= target <= nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            else:
                if nums[mid] <= target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1

        return -1

## 总结

这题做的还是非常混乱，感觉思路理不清，需要多做几次。