# 3 Sum

## Description

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

## 思路

这题最直观的解法应该是O(n^3),直接把所有可能的组合算起来，然后把所有为0的组合保存起来。
如果想要把时间复杂度缩短为O(n^2)的话，可以先直接求数组中的数两两相加是多少，然后用字典存起来。最后在遍历数组找有没有能够相加为0的元素。O(n)的算法暂时想不到。思路整体上没有太大问题，但是代码一直写不出来，之后参考了一下别人的代码。发现个人思路还是比较狭窄，我已经想到了要两个数相加的这一步，但是如何避免重复一直没有好的想法。一个比较好的方法就是先对数组进行排序，这样的话可以根据当前数字的大小来进行判断。因为如果我们在访问第i个数的话，那么前面的i-1个的值我们已经考虑过了，只需要解决第i个的问题就好了。

## 代码

```
class Solution:
    def threeSum(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        res = []
        for i in range(len(nums)-2):
            if i == 0 or nums[i] > nums[i-1]:
                left = i + 1; right = len(nums) - 1
                while left < right:
                    if nums[left] + nums[right] == -nums[i]:
                        res.append([nums[i], nums[left], nums[right]])
                        left += 1; right -= 1
                        while left < right and nums[left] == nums[left-1]: left +=1
                        while left < right and nums[right] == nums[right+1]: right -= 1
                    elif nums[left] + nums[right] < -nums[i]:
                        while left < right:
                            left += 1
                            if nums[left] > nums[left-1]: break
                    else:
                        while left < right:
                            right -= 1
                            if nums[right] < nums[right+1]: break
        return res
```

## 总结

