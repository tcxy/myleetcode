# First Missing Positive

## Description

Given an unsorted integer array, find the smallest missing positive integer.

Note:

Your algorithm should run in O(n) time and uses constant extra space.

## 思路

这道题的意思是，从1开始，寻找数组中缺失的数。难点有两个，一是O(n)，二是常数空间占用。要基于O(n)，就要求只能进行一遍扫描。这一遍扫描的重点是寻找缺口，因为要求是正的缺失数。所以可以从1来进行扫描，如果1不存在，那这个数就是1。如果1存在，就往上找。考虑到只能扫描一遍，并且要判断出缺失的数至少还需要另外一个数来进行判断。也就是说，关键在于找到比这个缺失的数小1的数。挣扎了一下还是没有想到好的解决方案，看了一下其他人的解法，大致意思就是让数组的第i个位置放i+1这个值，如果某个值超过了数组长度或者为0那就不管。这样换完了之后一定是从1开始的一个数组，只要找到哪个位置的值不是i+1，就返回i+1就可以了。

## 代码

```
class Solution:
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        i = 0
        while i < len(nums):
            if 0 < nums[i] < len(nums) and nums[i] != nums[nums[i] - 1]:
                temp = nums[nums[i] - 1]
                nums[nums[i] - 1] = nums[i]
                nums[i] = temp
            else:
                i += 1
        for i in range(len(nums)):
            if nums[i] != i + 1:
                return i + 1
        return len(nums) + 1
```

## 总结

这题最需要注意的就是while内部的判断，最开始的时候我写的for循环，但是提交的时候出错了。原因在于，交换之后，比如原本1就在后面，然后某次交换完了1到了前面，但是前面已经走过了，这时候1就不会被排在数组第一个元素了。当然我这么做的话，复杂度可能会高一点，但是应该控制在常数级别了，所以还是算O(n)