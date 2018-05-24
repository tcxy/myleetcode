# Spiral Matrix

## Description

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

## 思路

个人感觉访问主要是基于顺序来的，比如先从上面向右，然后向下，再向左，最后向上。按照这个顺序可以写出一种代码来，主要就是需要一个变量记录向哪里走，然后一个变量记录在第几层。

## 代码

``` python
class Solution:
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        res = []
        while matrix:
            res += matrix.pop(0)
            if matrix and matrix[0]:
                for row in matrix:
                    res.append(row.pop())
            if matrix:
                res += matrix.pop()[::-1]
            if matrix and matrix[0]:
                for row in matrix[::-1]:
                    res.append(row.pop(0))
        return res
```

## 总结

最开始准备根据规律去写，但是那样写太麻烦，总是出现条件错误，就直接借助python的特性做了。实际上的话，这道题两个变量应该不太够用，因为要不断变化值。最好还是四个变量，分别表示上下左右走到了哪里，然后根据这四个变量来决定每个循环内部怎么走。单次循环直接走完一轮，直到这四个值开始出现某几个值相等为止。