# Pascal's Triangle

## Description

Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

## 思路

这道题其实也是DP最简单的应用，直接构建好数组，然后第一个元素和最后一个元素设置为1。在往后根据具体的数来算就可以了。

## 代码

``` python
class Solution(object):
    def generate(self, numRows):
        """
        :type numRows: int
        :rtype: List[List[int]]
        """
        res = []
        for i in range(numRows):
            layer = i + 1
            nums = [0] * layer
            nums[0] = 1
            nums[layer - 1] = 1
            for j in range(1, layer - 1):
                nums[j] = res[i-1][j - 1] + res[i-1][j]
            res.append(nums)
        return res
```