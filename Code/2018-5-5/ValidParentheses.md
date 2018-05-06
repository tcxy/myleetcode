# Valid Parenthese

## Description

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

    Open brackets must be closed by the same type of brackets.
    Open brackets must be closed in the correct order.

Note that an empty string is also considered valid.

## 思路

这道题思路不难，而且判断方法很多。最简单的方法应该就是直接从左向右判断，然后每找到一个左边的符号就压入栈，如果遇到右边的符号，就从栈里面取出一个符号进行比对。相匹配就继续，不匹配就返回False，最后直接返回True。

## 代码

```
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        parentheses = {'(': ')', '{': '}', '[': ']'}
        left = []
        for char in s:
            if char in parentheses:
                left.append(char)
            else:
                if len(left) and char == parentheses[left.pop()]:
                     continue
                else:
                    return False
        return True if len(left) == 0 else False
```

## 总结

这题还是很简单的，就是需要注意最后的判断，因为有可能多出来一个左边的括号，所以最后要判断下left是否为空。