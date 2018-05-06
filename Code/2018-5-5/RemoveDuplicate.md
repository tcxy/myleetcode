# Remove Duplicates From Sorted Array

## Description

Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

## 思路

这题不难，麻烦的就是要求在原数组上进行操作，如果是C/C++倒是很简单，因为数组索引就是指针，可以直接通过索引来修改具体的值。另外由于要求O(1)的空间，基本上就是一个字符判断重复一个数字判断当前的位置问题了。

## 代码

```
class Solution:
    def removeDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 0:
            return 0
        
        dup_index = 0
        for index, value in enumerate(nums):
            if not value == nums[dup_index]:
                dup_index += 1
                nums[dup_index] = value
        return dup_index + 1
```

## 总结

感觉主要是[]这种数组的结果需要特别注意下。