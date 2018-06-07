# Nth Digit

## Description

Find the nth digit of the infinite integer sequence 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, ... 

## 思路

实际上就是寻找第n个数字，但是每个数字都只能是0-9，所以必须要找。brute-force应该直接从1到n，然后计算当前走过的数字就行了。我个人采用的方法是直接寻找比较近的一个地方，比如n是300的时候，从1到10到100，n就在这个区间内部。然后看100对应有多少位，再来计算n到底是哪个数字。但是这种情况可能会出现n在100的左侧，比如100，101。或者n在100的右侧，像是700等。之后我觉得还是固定在一边会比较好，所以从0-9开始，每走过一段就让n减去相应的值。直到n的值没办法走过当前这一段的时候，就可以确认n在右侧。由于n的值在变，所以需要记录一下起点。不过起点是比较好计算的，因为从1开始，10，100。

## Code

``` python
class Solution:
    def findNthDigit(self, n):
        """
        :type n: int
        :rtype: int
        """
        step = 9
        start = 1
        size = 1
        while n > size * step:
            n -= size * step
            start *= 10
            size += 1
            step = step * 10
        return ((start + (n-1)//size) // 10**(size-1-(n-1)%size)) % 10
```