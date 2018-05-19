# Permutations

## Description 

Given a collection of distinct integers. return all possible permutations.

## 思路

如果直接做这题的话，相当取一个值然后再慢慢取后面的值，这里应该有点像递归，不断走下去，然后到了最后加入数组。这样做的话，时间复杂度应该会比较大，但是应该没有其他特别好的方案。试了一下之后发现达到了maximum recursion，感觉还是有点问题。借鉴了一下其他人的思路，大体上就是，像这样的问题，我们可以先假设已经存在一个结果result。这个result放着的是当前已经遍历过的数字可以构成的结果，比如1只存在[1]一种，但是1和2就有[1,2]以及[2,1]两种情况。如果这个时候再来一个数字3，那么对于result中的两个数组，3可以存放的位置有1，2，3三种情况，即当前数组的长度+1。由此对于result中的每个数组，我都需要创建3个新的数组。通过python的slice，可以很好的进行拼接。

## 代码

``` python
class Solution；
    def permute(self, nums):
    """
    :type nums: List[int]
    :rtype: List[List[int]]
    """
    results = [[]]
    for n in nums:
        temp_result = []
        for result in results:
            for i in range(len(result) + 1):
                temp_result.append(result[:i] + [n] + result[i:])
        results = temp_result
    return results
```

## 总结

这种方法在很多地方都可以用，比如之前做过的生成括号等等。