# Maximum Depth of Binary Tree

## Description

Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

## 思路

这题还是可以按照我之前的Zigzag那个思路来写，因为这里需要返回的是n，所以直接根据n来改就好了。

## 代码

``` python
class Solution:
    def maxDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if not root:
            return 0
        cur = []
        nex = [root]
        return self.traverseLevel(nex, [], 1)
    
    def traverseLevel(self, cur, nex, n):
        if len(cur) == 0:
            return n - 1
        length = len(cur)
        for i in range(len(cur)):
            node = cur.pop()
            if node.left:
                nex.append(node.left)
            if node.right:
                nex.append(node.right)
        return self.traverseLevel(nex, cur, n + 1)
```