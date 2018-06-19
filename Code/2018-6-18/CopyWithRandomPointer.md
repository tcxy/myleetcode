# Copy List with Random Pointer

## Description

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

## 思路

这个题目，最开始的感觉是遍历两遍然后一次next一次random就行。但是考虑到链表的访问机制，时间开销应该会很大。而且题目没有给出用例，不清楚会不会出现链表中有相同元素的情况。加入不存在重复元素的话，比较掏巧的一个方法就是通过list来辅助实现，这样的话list的每个元素都是一个链表。然后通过一个字典来记住对应元素所处的位置。遍历第一遍构建新链表之后，就可以通过第二次遍历以及字典和list来构建random指针。参考了一下另一种方法，并不需要其它的结构来帮忙，主要思路是利用新旧交替，也就是把新的结点插入在原结点的next，这样链表中长度会变成原来的两倍，比如l1和l2是两个相邻的结点，那么l1是旧结点，而l2是新节点。l1.random指向的是旧链表中的random指针，那么新节点中的random就是它对应的下一位。最后再把新链表构建起来旧可以了。坏处就是原结点发生了改变，当然，也可以同时修改新旧结点，使旧结点维持原样。

## 代码

``` python
# Definition for singly-linked list with a random pointer.
# class RandomListNode(object):
#     def __init__(self, x):
#         self.label = x
#         self.next = None
#         self.random = None

class Solution(object):
    def copyRandomList(self, head):
        """
        :type head: RandomListNode
        :rtype: RandomListNode
        """
        if head == None:
            return None
        node = head
        while node != None:
            newNode = RandomListNode(node.label)
            newNode.next = node.next
            node.next = newNode
            node = newNode.next
        node = head
        while node != None:
            newNode = node.next
            if node.random:
                newNode.random = node.random.next
            node = node.next.next
        newHead = head.next
        newnode = head.next
        oldnode = head
        while newnode.next:
            oldnode.next = newnode.next
            oldnode = oldnode.next
            newnode.next = oldnode.next
            newnode = newnode.next
        newnode.next = None
        oldnode.next = None
        return newHead
```

## 总结

这道题主要还是对链表的掌握，需要注意三次循环的时候具体的顺序。