# Trapping Rain Water

## Description

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

## 思路

感觉可以直接用一层循环，然后在循环的时候把每一个非0的值当作左值来求右值，根据左右值来决定高度会是多少，然后求体积。实际代码写的时候还是会有问题，比如32120这样子的，就不太好判断到底哪个是左值，哪个是右值。看了一下别人的代码，分析了一下思路。主要是从左往右走的时候，只要右边的值能够比左边大，那么从左边这个值开始，沿途走过的所有比左边值小的点，一定能够包含左边减去点对应值的水。所以这个问题就相当于从左右两边向中间扫描，直到这两个数相等为止。

## 代码

```
class Solution:
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        left = 0
        right = len(height) - 1
        result = 0
        if len(height) < 3:
            return 0
            
        while left < right:
            left_value = height[left]
            right_value = height[right]
            if left_value <= right_value:
                left += 1
                while left < right and left_value >= height[left]:
                    result += left_value - height[left]
                    left += 1
            else:
                right -= 1
                while left < right and right_value >= height[right]:
                    result += right_value - height[right]
                    right -= 1
        return result
```

## 总结

这个题目确实很难，思路上其实有点像脑筋急转弯。很容易陷入误区，再一个就是各个条件的判断，比如我的left+1和right-1有两处都需要写。