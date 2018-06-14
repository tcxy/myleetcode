# Populating Next Right Pointers in Each Node

## Description

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

## 思路

个人感觉这道题还是需要按照层数来进行遍历，所以还是和之前的那些题目写法相同。只不过按层数访问的时候，修正一下指针。

## 代码

``` python
class Solution:
    # @param root, a tree link node
    # @return nothing
    def connect(self, root):
        if not root:
            return 
        self.traverseLayer([root], [])
        
    def traverseLayer(self, cur, nex):
        if len(cur):
            for i in range(len(cur)):
                if not i == len(cur) - 1:
                    cur[i].next = cur[i + 1]
                else:
                    cur[i].next = None
                if cur[i].left:
                    nex.append(cur[i].left)
                if cur[i].right:
                    nex.append(cur[i].right)
            self.traverseLayer(nex, [])
```

测试之后通过，但是执行时间不太理想。

## 代码2

``` python
 class Solution(object):
    def connect(self, root):
        """
        :type root: TreeLinkNode
        :rtype: nothing
        """
        
        if not root:
            return None
        cur  = root
        next = root.left

        while cur.left :
            cur.left.next = cur.right
            if cur.next:
                cur.right.next = cur.next.left
                cur = cur.next
            else:
                cur = next
                next = cur.left
```

## 总结

实质上这道题还是和层数相关，但是并不需要额外空间和递归。因为每一次都是从最左边走到最右边，并且当两个树之间存在间隙的时候，可以通过他们的父结点联系起来。