# Best Time to Buy and Sell Stock II

## Description

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

## 思路

和之前那道题差不多，但是可以购买并卖出多次了。本来没什么思路，但是随便写了一下也过了。

## 代码

``` python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        maxprofile = 0
        for i in range(1, len(prices)):
            if prices[i] > prices[i - 1]:
                maxprofile += prices[i] - prices[i - 1]
        return maxprofile
```

## 总结

具体是什么原因我也不是特别清楚，就是随便分析了下写出来发现可以通过。我估计是因为重点在于差值，之前我一直在考虑如果遇到了特殊情况会怎么样。但是实际上各种情况都可以拆分，比如[5,8,9,10]，这样的数组按照算法其实在一直重复计算，比如从8-5，到9-8，到10-9，实际上这个值就是5-10。故而这个算法应该是OK的。