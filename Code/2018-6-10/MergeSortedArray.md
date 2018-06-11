# Merge Sorted Array

## Description

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:

    The number of elements initialized in nums1 and nums2 are m and n respectively.
    You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.

## 思路

已经sort好的数组合并，主要就是考虑当前插入哪一个值就可以了。后来写的时候发现特别麻烦，因为有时候可能存在当前nums1的某个位置要插入nums2的值，但是此时在nums1中的值需要找个位置插入。所以改用从尾部开始循环。

## 代码

``` python
class Solution:
    def merge(self, nums1, m, nums2, n):
        """
        :type nums1: List[int]
        :type m: int
        :type nums2: List[int]
        :type n: int
        :rtype: void Do not return anything, modify nums1 in-place instead.
        """
        l = m - 1
        r = n - 1
        while l >= 0 and r >= 0:
            if nums1[l] <= nums2[r]:
                nums1[l + r + 1] = nums2[r]
                r -= 1
            else:
                nums1[l + r + 1] = nums1[l]
                l -= 1
        if r >= 0:
            nums1[:r+1] = nums2[:r+1]
```