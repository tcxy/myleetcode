# Binary Tree Level Order Traversal

## Description

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

## 思路

这道题的要求就是按照树的层级来排，关键问题就是什么时候进入下一层。按照二叉树的特性，root下面有两个子树，然后再往下是四层。这里应该可以用栈来解决要访问的结点问题，一共应该需要两个栈，一个cur，一个next，cur中存放当前需要访问的结点，然后每访问一个结点，就把其子树全部压入next。当cur为空的时候，就把next赋值给cur，直到cur为0为止。

## 代码

``` python
class Solution:
    def levelOrder(self, root):
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
        self.traverseLevel(nex, [], res, layer)
        return res
    
    def traverseLevel(self, cur, nex, res, layer):
        if len(cur) == 0:
            return
        
        while len(cur) > 0:
            node = cur.pop(0)
            layer.append(node.val)
            if node.left:
                nex.append(node.left)
            if node.right:
                nex.append(node.right)
        res.append(layer)
        layer = []
        self.traverseLevel(nex, cur, res, layer)
```