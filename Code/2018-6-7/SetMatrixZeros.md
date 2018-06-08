# Set Matrix Zeros

## Description

Given a m x n matrix, if an element is 0, set its entire row and column to 0.

## 思路

这题基本上还是需要去对比才行。in place其实很好做，关键看能不能有更好更高效的方案。

## 代码

``` python
class Solution:
    def setZeroes(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: void Do not return anything, modify matrix in-place instead.
        """
        m = len(matrix)
        if m == 0:
            return
        n = len(matrix[0])
        if n == 0:
            return
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == 0:
                    self.changeRow(i, n, matrix)
                    self.changeCol(m, j, matrix)
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == 'a':
                    matrix[i][j] = 0
    
    def changeRow(self, m, n, matrix):
        for i in range(n):
            matrix[m][i] = 'a' if matrix[m][i] != 0 else 0
    
    def changeCol(self, m, n, matrix):
        for i in range(m):
            matrix[i][n] = 'a' if matrix[i][n] != 0 else 0
```

## 总结

这题暂时没有看到比较好的方案，其实都需要遍历然后去找哪些需要改，然后最后又要遍历一次来完成替换。