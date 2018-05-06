# Merge k Sorted Lists

## Description

Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

## 思路

这题感觉不太好有思路，尤其是要考虑复杂度的情况下。不过因为我用python，所以可以有一些比较猥琐的解法。比如直接取出所有的值放在数组里排序，然后再创建一个新的链表。但是，这样子复杂度其实是无法确定的。个人感觉这题的复杂度非常难确定，因为具体有多少个数字我根本没办法知道。随便试了一下没想到直接过了，不过具体的算法还是要好好学习才行。

## 代码

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        head = ListNode(0)
        node = head
        nums = []
        for li in lists:
            while li:
                nums.append(li.val)
                li = li.next
        nums.sort()
        for i in nums:
            node.next = ListNode(i)
            node = node.next
        return head.next
```

## 具体算法思路

看了下，这道题的算法思路可以有两种。一种是利用分治来解决问题，这样就把k个list分成两两一组或者单独一个为一组，然后就回到了两个链表合并的情况了。等到k缩小为1的时候，也就得到了最终要的结果。另一种则是利用了最小堆的结构，每一次都获取首个元素加入堆中，然后取出最小的那一个加入链表。一直到堆空了为止，这个方法和我用的其实差不多，只不过我一次性加入了所有的元素，然后利用python内置的排序来完成结果。最小堆的排序其实也是log(n)级别的。

## 分治算法

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        if len(lists) == 0:
            return None
        n = len(lists)
        while n > 1:
            k = (n + 1) // 2
            for i in range(n // 2):
                lists[i] = self.mergeTwoLists(lists[i], lists[i + k])
            n = k
        return lists[0]
    
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        head = ListNode(0)
        node = head
        while l1 and l2:
            node.next = ListNode(0)
            node = node.next
            if l1.val < l2.val:
                node.val = l1.val
                l1 = l1.next
            else:
                node.val = l2.val
                l2 = l2.next
        if l1:
            node.next = l1
        if l2:
            node.next = l2
        return head.next
```

分治算法其实python中唯一需要注意的就是/和//的问题了，另外就是速度会很慢。