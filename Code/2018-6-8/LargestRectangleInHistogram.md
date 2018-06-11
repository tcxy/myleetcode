# Largest Rectangle in Histogram

## Description

Given n non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

## 思路

这个题和之前做过的一系列以一组矩形为输入，按照面积来比较的题目相同，基本思路也一样，从left和right开始做就行了。实际写了代码之后发现还是有问题，这题其实如果用O(N^2)的话会非常好写，但是个人还是希望能够掌握一下算法的思路。

## 代码

``` python
class Solution:
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        heights.append(0)
        stack = [-1]
        ans = 0
        for i in range(len(heights)):
            while heights[i] < heights[stack[-1]]:
                h = heights[stack.pop()]
                w = i - stack[-1] - 1
                ans = max(ans, h * w)
            stack.append(i)
        heights.pop()
        return ans
```

## 总结

heights加0主要是为了走到数组结尾的时候强制运算一次，确保能够留住所有结果。stack的作用主要是回溯，其中保留的值是下标。stack中的-1应该是保证这个值一直存在于栈底，当当前访问的值大于栈顶的值的时候，就计算栈中当前存好的数据的面积，结束后存入新的index。这个题目主要是利用栈中的升序排列来进行，为了不错过后面的一些值，会比较当前值和栈顶值的大小，这样就不会错过某些值。