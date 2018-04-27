# Median of Two Sorted Arrays

## Description

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

## 思路

这题目的难点在于O(log (m+n))，也就是差不多刚好遍历两个数组。个人觉得可以新建一个数组来存储最后的结果，然后开始遍历数组A，在遍历数组A的时候可以用另一个值来表示数组B当前访问到第几个数了，然后数组A每访问一个数，根据A中的数和B中的数来判断哪个应该在前，以及B中的数是否要插入新的数组中。当然，这里还要判断一下数组中的最后一个数是多少，以免出现B中的某个数应该排在A中某几个数之后的情况。

## 代码

```

class Solution(object):
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        result_array = [] # Store all the number in num1 and num2, sorted
        length = 0 # Indicate how many numbers in result_array
        length1 = len(nums1) # The length of nums1
        length2 = len(nums2) # The length of nums2
        sub1 = 0 # Subscript for nums1
        sub2 = 0 # Subscript for nums2
        while sub1 != length1 or sub2 != length2:
            num1 = nums1[sub1] if sub1 <= length1 - 1 else float('inf')
            num2 = nums2[sub2] if sub2 <= length2 - 1 else float('inf')
            if num1 <= num2 or sub2 == length2:
                result_array.append(num1)
                sub1 += 1
            elif num2 < num1 or sub1 == length1:
                result_array.append(num2)
                sub2 += 1
            length += 1
        if length % 2 == 0:
            median = length / 2
            return (result_array[median - 1] + result_array[median]) / 2.0
        else:
            return result_array[length // 2]
```

## 总结

可以说是写得非常波折了，其实思路不难，仔细点可以一遍写好不出bug。但是写着写着就容易堵了，结果调试时间比我看题写代码时间还长。当然最蛋疼的是，我看到有人直接把num1 extend了，然后直接sorted求解。仔细想想这么写也确实符合要求来的。。。