# Add Two Numbers

## Description

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

## 思路

其实就是用链表表示的两个数相加，不过这里并没有提及两个链表是否长度相等，故而代码中需要注意长度问题。
这题个人思路有几种：将两个数分别求出来然后相加，最后的值再按%10来转化成链表；直接访问两个链表，然后将结果存到一个新链表中，然后返回结果。两种方法都是O(n)，当然，第一种方法花费时间是要多一些的。
这题另一个要注意的点就是ListNode是个自定义的结构，以注释的形式出现在开头。

## 代码

```

# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        # create a new ListNode to store the result
        result = sum = ListNode(0)
        add = 0
        while l1 or l2 or add:
            if l1:
                add += l1.val
                l1 = l1.next
            if l2:
                add += l2.val
                l2 = l2.next
            sum.next = ListNode(add % 10)
            sum = sum.next
            add //= 10
        return result.next
```

## 总结

基本上这题不会有其他的解法了，链表的遍历只能靠结点不断后移来实现。提交之后看最终答案也差不多是这样，但是这题目其实还有几个坑，一个是Python3里面/除法是会直接带小数的，如果想直接获取首位数字的话还是需要用//。当然，因为都是个位数相加，所以求出余数之后直接减去余数也是可以的。还有一点就是链表的时候，这里我用了两个变量在开头去标记链表的表头，主要原因是单向链表的结点往后走了就回不来了，所以还需要留一个指向表头的结点来返回结果。这个问题中最容易犯的毛病应该是我算法中写的add，链表的遍历主要取决于结点什么时候为空属于常识，但是在注意到循环终止条件后非常容易忽略题目中的加法要求。那就是最后一位是需要进位的，一个比较简单的例子就是5和5，相加结果为10，返回的内容应该是[0,1]，但是一个不注意就会返回0，我也在这里栽了个跟头。