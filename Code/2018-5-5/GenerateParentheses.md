# Generate Parentheses

## Description

 Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is: 

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

## 思路

这题我唯一想到的就是采用递归的形式来完成，基本上可以分为一个left和right，然后left和right可以包含n个对应的括号。每执行一次就从left或者right中来取出一个括号，然后当left和right都为空的时候直接把字符串加入数组。

```
class Solution:
    def generateParenthesis(self, n):
        """
        :type n: int
        :rtype: List[str]
        """
        def parens(str, left, right, result=[]):
            if left:         
                parens(str + '(', left-1, right)
            if right > left: 
                parens(str + ')', left, right-1)
            if not right:    
                result.append(p)
                return result
        return parens('', n, n)
```

## 总结

递归的时候可能会有点绕，主要需要记住括号一定是从左边开始右边结束。所以重点是先生成左边再生成右边，也就是说，如果右边对应的数字大，那就要生成右边。等到左右都为空了，就可以加入数组了。