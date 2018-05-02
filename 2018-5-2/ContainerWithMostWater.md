# Container With Most Water

## Description

Given n non-negative integers a1, a2, ..., an, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

Note: You may not slant the container and n is at least 2. 

## 思路

这题目出得非常绕口，很容易搞迷糊。说白了就是给你一列数组，然后你需要求的是，在这一列数组中找出两个数，使得他们的下标之差乘以这两个数中比较小的那个值所得的结果最大。这题最直观的解法应该就是直接用两个循环嵌套，时间复杂度为O(n ^ 2)。不过看问题是Medium估计肯定不会这么简单让人过，试了一下果然直接超时。问题的关键应该是怎么在O(n)内搞定，如果想O(n)说白了就是只能够遍历一次。遍历一次的话最大的问题在于怎么去访问这个数组，因为这个问题的最大取决于乘积，所以最终的结果不见得是数组的两端。故而怎么找到下一个需要访问的下标很重要。个人最初的想法是按照最大值来考虑，比如我从两端开始访问这个数组，如果右边走一格结果会比当前的最大值大，那么我就把右边的值向左走一步。如果左边走一格结果会比当前大，那么我就把左边的值向右走一步。仔细想想这个结果应该行不通，最极端的情况，比如[3,1,20,20,2,2],最开始在两端的时候最大值为5 * 2 = 10，然后左右都不会走了，但是实际上的最大值应该是中间的[20,20]才对。但是左右同时走也不行，如果最大的两个值并不堆成，那么结果还是错误的。考虑的重点应该可以分为当我移动之后面积大于max，和移动之后面积小于max的情况。大于max肯定直接移动，小于max可以考虑两边同时移动。但是大于max的移动也要看考虑移动哪一边，到底是先移动左边还是右边。这里的话应该可以按照大小来考虑，优先移动小的一边。尝试之后代码还是有点错，仔细回顾了一下。其实不需要考虑大于max或者小于max的问题，因为我的目的是遍历数组。所以直接按照左边右边的大小来决定移动哪边，在移动的时候终止条件应该是数值，毕竟在移动过程中面积对应的length一定是在减小的，所以要获取最大值一定需要高度上的变化。也就是说我只要不断的寻找到下一个比当前值大的数值就可以了。

## 代码

```
class Solution:
    def maxArea(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        left = 0
        right = len(height) - 1
        result = 0
        
        while left < right:
            l_value, r_value = height[left], height[right]
            length = right - left
            result = max(result, length * min(l_value, r_value))
            if l_value < r_value:
                while height[left] <= l_value and left < right:
                    left += 1
            else:
                while height[right] <= r_value and right > left:
                    right -= 1
        return result
```

## 总结

这道题我个人觉得其实不难，重点在于思考的方向。目前为止的题目我拿到手首先考虑的就是循环问题，但是像这样的题目其实直接提取公式会更好判断。这题里面的公式其实就是area = length * height，height由两个值中最小的那一个决定，而length则由两个值的索引之差来决定。如果从这个公式入手的话会好不少，因为这样我们需要考虑的只有两个值，一个是length一个是height。height最长我们不知道，但是length最长就是数组的长度。也就是说无论怎么变，length一定是小于等于数组长度的，既然length会变小，那么最大值如果不是数组两个边界的时候意味着height变大了。故而思路转向怎么求height的最大值，而height又是由数组中两个值里最小的那个决定的，所以思路应该转向怎么提高两个数中的最小值。这样，代码其实基本就写出来了。