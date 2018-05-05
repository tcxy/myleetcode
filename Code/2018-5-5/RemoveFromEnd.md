# Remove Nth Node from End of List

## Description

Given a linked list, remove the n-th node from the end of list and return its head.

## 思路

这题要求只能遍历一遍，但是要删除的结点是从后往前数的。个人感觉有点像是用一个列表去存链表中的每一项，然后完了直接按照长度来删除相应的结点，这样就可以在一次遍历中搞定全部。缺点就是空间占用会比较大。

## 代码

```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def removeNthFromEnd(self, head, n):
        """
        :type head: ListNode
        :type n: int
        :rtype: ListNode
        """
        nodes = []
        node = head
        while node:
            nodes.append(node)
            node = node.next
        
        length = len(nodes)
        if length - n == 0:
            # Delete head
            head = head.next
        else:
            deleteNode = nodes[length - n - 1]
            nextNode = deleteNode.next
            if nextNode:
                deleteNode.next = nextNode.next
            else:
                deleteNode.next = None
        return head
```

## 总结

整体来说，这题不难。需要注意的地方在于，当删除的结点位于头节点或者尾结点的时候要怎么办。因为普通的删除是找到要删除结点的前一个，然后把这个结点的next连接到要删除结点的后一个上。但是对于头和尾部来说会缺少相应的结点，所以要做单独判断。