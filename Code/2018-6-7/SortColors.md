# Sort Colors

## Description

Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

## 思路

这个题感觉就是一般的排序题，直接快排应该就可以了。

## 代码

``` python
class Solution:
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        low, high = 0, len(nums) - 1
        self.quick_sort(nums, low, high)
                
    def quick_sort(self, array, left, right):  
        if left >= right:  
            return  
        low = left  
        high = right  
        key = array[low]  
        while left < right:  
            while left < right and array[right] > key:  
                right -= 1  
            array[left] = array[right]  
            while left < right and array[left] <= key:  
                left += 1  
            array[right] = array[left]  
        array[right] = key  
        self.quick_sort(array, low, left - 1)  
        self.quick_sort(array, left + 1, high)  
```

### 其他案例

``` python
class Solution:
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        pivot = 1
        s, e, l = 0, 0 , len(nums) - 1
        
        while e <= l:
            if nums[e] < pivot:
                nums[s], nums[e] = nums[e], nums[s]
                s += 1
                e += 1
            elif nums[e] == pivot:
                e += 1
            else:
                nums[l], nums[e] = nums[e], nums[l]
                l -= 1
```

## 总结

这题的本质就是排序，但是其他人给出的这个方案我觉得很有意思，也很适合这个题目。AC算法