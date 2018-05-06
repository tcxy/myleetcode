# Merge Two Sorted Lists

## Description

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## 思路

应该没什么好说的，直接用Node来判断进行比较就行了。

## 代码

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
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

## 总结

这题关键其实就是循环，只要注意到了循环的条件就好。如果以与为判断条件，那么结尾再做判断就行了。如果想用或做判断条件的话，那只能在循环内部写地复杂点了。看了discussion之后还是发现了一些非常有趣地解法。

## 代码2

```
class Solution:
    def mergeTwoLists(self, a, b):
        if a and b:
            if a.val > b.val:
                a, b = b, a
            a.next = self.mergeTwoLists(a.next, b)
        return a or b
```

采用了递归，每一次都把相对小的Node放在前面，然后一遍遍走下去。