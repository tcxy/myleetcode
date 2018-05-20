# Rotate Image

## Desciption

You are given an n x n 2D matrix representing an image

Rotate the image by 90 degress (clockwise)

## 思路

这个题目要求直接在矩阵中进行变换，不能用另外一个矩阵来做。主要思路的话，如果顺时针旋转90度，其实相当于直接把这个矩阵做一个reverse，接下来直接做一个镜像就好了。

## 代码

``` python
class Solution:
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        length = len(matrix)
        for i in range(length):
            matrix[i].reverse()
        for i in range(length):
            for j in range(length - i):
                matrix[i][j], matrix[length - j - 1][length - i - 1] = matrix[length - j - 1][length - i - 1], matrix[i][j]
```

## 总结

这道题需要比较灵活的使用翻转会比较快。