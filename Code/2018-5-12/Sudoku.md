# Valid Sudoku

## Description

Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

    Each row must contain the digits 1-9 without repetition.
    Each column must contain the digits 1-9 without repetition.
    Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.


## 思路

这个题目主要是做一个棋盘的检查，只要保证每一行的数字只会出现一个，并且在3x3里面也只会出现一次就行了。

## 代码

```
class Solution:
    def isValidSudoku(self, board):
        def is_valid_row(board):
            for row in board:
                if not is_valid(row):
                    return False
            return True
        
        def is_valid_column(board):
            for col in zip(*board): 
                if not is_valid(col):
                    return False
            return True
        
        def is_valid_square(board):
            for i in (0,3,6):
                for j in (0,3,6):
                    square = [board[x][y] for x in range(i,i+3) 
                                        for y in range(j,j+3)]
                    if not is_valid(square):
                        return False
            return True
    
        def is_valid(value):
            res = [i for i in value if i != '.']
            return len(res) == len(set(res))
    
        return is_valid_row(board) and is_valid_column(board) and is_valid_square(board)
```

## 总结

写的有点麻烦了，但是我个人觉得行，列和小棋格都是必须检查的。

## 其他人的代码

```
class Solution:
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        dic_row = [{},{},{},{},{},{},{},{},{}]
        dic_col = [{},{},{},{},{},{},{},{},{}]
        dic_box = [{},{},{},{},{},{},{},{},{}]

        for i in range(len(board)):
            for j in range(len(board)):
                num = board[i][j]
                if num == ".":
                    continue
                if num not in dic_row[i] and num not in dic_col[j] and num not in dic_box[3*(i//3)+(j//3)]:
                    dic_row[i][num] = 1
                    dic_col[j][num] = 1
                    dic_box[3*(i//3)+(j//3)][num] = 1
                else:
                    return False

        return True
```

看了很久，这份代码应该是我最喜欢的，速度快，而且相对简洁。只需要一重循环就可以解决问题，虽然空间开销比较大。