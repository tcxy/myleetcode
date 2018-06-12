# Binary Tree Zigzag Level Order Traversal

## Description

Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

## 思路

这题基本和上一题解法一致，但是我要加入一个新的变量记录层数。然后根据层数的奇偶性来决定要回溯的方向。

## 代码

``` python
class Solution:
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if not root:
            return []
        res = []
        layer = []
        cur = []
        nex = [root]
        self.traverseLevel(nex, [], res, layer, 1)
        return res
    
    def traverseLevel(self, cur, nex, res, layer, n):
        if len(cur) == 0:
            return
        length = len(cur)
        layer = [0] * length
        for i in range(length):
            node = cur.pop(0)
            pos = length - i - 1 if n % 2 == 0 else i
            layer[pos] = node.val
            if node.left:
                nex.append(node.left)
            if node.right:
                nex.append(node.right)
        res.append(layer)
        layer = []
        self.traverseLevel(nex, cur, res, layer, n + 1)
```