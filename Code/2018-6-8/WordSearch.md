# Word Search

## Description

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

## 思路

这个题感觉主要是先找到对应的第一个字符，然后横向或者纵向执行，直到到了边界或者是字符不匹配了，然后尝试改变方向。麻烦之处在于遍历的方向有四个，但是每次遇到了不对应的字符，都是需要从四个方向来考虑，所以这可以构成一个递归。

## 代码

``` python
class Solution:
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        cur = 0
        for i in range(len(board)):
            for j in range(len(board[0])):
                if self.find(board,word, i, j):
                    return True
        return False
                    
    def find(self, board, word, i, j):
        if len(word) == 0:
            return True
        if i < 0 or i >= len(board) or j < 0 or j >= len(board[0]) or word[0] != board[i][j]:
            return False
        temp = board[i][j]
        board[i][j] = '#'
        res = self.find(board, word[1:], i+1, j) or self.find(board, word[1:], i - 1, j) or self.find(board, word[1:], i, j + 1) or self.find(board, word[1:], i, j - 1)
        board[i][j] = temp
        return res
```