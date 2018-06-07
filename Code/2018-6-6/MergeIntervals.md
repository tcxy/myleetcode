# Merge Intervals

## Description

Given a collection of intervals, merge all overlapping intervals.

## 思路

这个题目如果在面试的时候被问到，第一反应应该是问一下具体的用例，因为给出的collection如果是有一定规律的，比如按照大小来排，那么对具体的算法还是有很大的影响。仔细考虑了一下，能够直接让这些元素按照大小来排对最终的解法还是有很大的帮助，所以直接尝试一下能不能先排序。之后直接合并就行了。

## 代码

``` python
class Solution:
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        if len(intervals) == 0:
            return []
        intervals = sorted(intervals, key = lambda x: x.start)
        res = [intervals[0]]
        for interval in intervals[1:]:
            if interval.start <= res[-1].end:
                res[-1].end = max(interval.end, res[-1].end)
            else:
                res.append(interval)
        return res
```

## 总结

这题目有几个点要注意，一个是<=，另一个是在合并的时候要考虑到后一个可能包含在前一个里面的情况。