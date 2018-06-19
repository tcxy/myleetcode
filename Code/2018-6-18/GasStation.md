# Gas Station

## Description

There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once in the clockwise direction, otherwise return -1.

Note:

    If there exists a solution, it is guaranteed to be unique.
    Both input arrays are non-empty and have the same length.
    Each element in the input arrays is a non-negative integer.

## 思路

问题主要是需要顺时针行驶，所以可以直接从第0个元素开始遍历，一直到最后一个。基本思路是没有问题的，但是最终超时了。之后参考了一下别人的思路，这道题其实有更简单的做法。因为是顺时针运行的，所以直接计算tank的值。也就是加上某一点的gas再减去cost，如果在某一点这个值小于了0。说明到目前为止的循环是不能满足条件的，那么就重置tank并且从下一个值开始重新计算。当程序运行结束了时候，对应的position就是要求的值。当然，最终还需要再确认一次，以防这个点前面的cost太多。这里一个比较直接的方法就是比较总cost和总gas的值就可以了。

## 代码

``` python
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        index = 0
        tank = 0
        total = 0
        if len(gas) != len(cost):
            return -1
        for i in range(len(gas)):
            tank += gas[i] - cost[i]
            if tank < 0:
                total += tank
                tank = 0
                index = i + 1
        return -1 if total + tank < 0 else index
```