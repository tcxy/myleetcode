# Best Time to Buy and Sell Stock

## Description

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

## 思路

这道题需要两个参数来决定，一个是购买的时机，一个是卖出的时机。隐藏条件为卖出的时间必须在购买的时间之后，也就说，如果我开始遍历数据寻找购买的时间，那么卖出的时间要在这之后。反过来说，如果遍历数组寻找卖出的时机，只要知道前面的最小值就可以了。

## 代码

``` python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        minPrice = float('inf')
        maxProfile = 0
        for price in prices:
            minPrice = min(minPrice, price)
            profile = price - minPrice
            maxProfile = max(maxProfile, profile)
        return maxProfile
```