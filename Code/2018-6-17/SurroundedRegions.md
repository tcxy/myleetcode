# Surrounded Regions

## Description

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

## 思路

遍历的时候不需要考虑最外围的'O'。对于内层的'O'，先压入栈，然后从几个方向来看是否能够连接到边界，如果能够连接到边界，那么栈中所有的点都可以直接放入另一张表中。然后对于新的'O'，先检查它是否在新的表中。最后执行的时候出现超时，只能换用其他思路。可以考虑从四条边出发，如果四条边上的'O'附近有'O'就先一起变为'S'，到了最后再变回来。然后其他的'O'都变为'X'。

## 代码

``` python
class Solution(object):
    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        m = len(board)
        if m == 0:
            return
        n = len(board[0])
        if n == 0:
            return
        for i in range(n):
            if board[0][i] == 'O':
                self.changeSurround(board, 0, i)
            if board[m - 1][i] == 'O':
                self.changeSurround(board, m - 1, i)
        for i in range(m):
            if board[i][0] == 'O':
                self.changeSurround(board, i, 0)
            if board[i][n - 1] == 'O':
                self.changeSurround(board, i, n - 1)
        for row in board:
            for i, val in enumerate(row):
                if val == 'O':
                    row[i] = 'X'
                if val == 'S':
                    row[i] = 'O'

    def changeSurround(self, board, i, j):
        m = len(board)
        n = len(board[0])

        if i < 0 or i > m - 1 or j < 0 or j > n - 1:
            return
        if board[i][j] == 'O':
            board[i][j] = 'S'
            self.changeSurround(board, i - 1, j)
            self.changeSurround(board, i + 1, j)
            self.changeSurround(board, i, j - 1)
            self.changeSurround(board, i, j + 1)
```