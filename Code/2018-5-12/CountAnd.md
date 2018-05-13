# Count and Say

## Description

The count-and-say sequence is the sequence of integers with the first five terms as following:

``` python
1.     1
2.     11
3.     21
4.     1211
5.     111221
```

1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

## 思路

这题目我看了很久才明白在干啥，意思应该是最开始有一个1，然后第二项就是11，也就是第一项有一个1。第三项就是，第二项有两个1。也就说，如果有一个数字n，那么我需要知道前n-1个项才能知道如何搞定这个第n项。

## 代码

``` python
class Solution:
    def countAndSay(self, n):
        """
        :type n: int
        :rtype: str
        """
        result = '1'
        for _ in range(n - 1):
            pre = result
            result = ''
            i = 0
            while i < len(pre):
                char = pre[i]
                count = 1
                i += 1
                while i < len(pre) and pre[i] == char:
                    count += 1
                    i += 1
                result = result + str(count) + str(char)
        return result
```

## 总结

主要还是把思路理清了就行，这题做的时候n-1遍是必须有的。可以用递归也可以用循环来实现，循环内部实际上又是进行了一次遍历，中间主要是为了确认如何生成下一个字符串。