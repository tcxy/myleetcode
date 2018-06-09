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