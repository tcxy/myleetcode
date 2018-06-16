# Binary Tree Maximum Path Sum

## Description

Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

## 思路

这题其实只是单纯地求path并不难，但是这道题需要求的是任意两点之间的路径。而且需要的是最大路径，这时候可以分为几种情况，某个结点的左边是最大，其右边是最大，从其左边到右边是最大。一般来说，对于root结点，其左边的最大值和右边的最大值加上自己的值就是最大的。思路基本上没问题，但是回溯一直都有点问题。

## 代码

``` python
class Solution(object):
    def maxPathSum(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        def dfs(node):  # returns: max one side path sum, max path sum
            l = r = 0
            ls = rs = None
            if node.left:
                l, ls = dfs(node.left)
                l = max(l, 0)
            if node.right:
                r, rs = dfs(node.right)
                r = max(r, 0)
            return node.val + max(l, r), max(node.val + l + r, ls, rs)
        if root:
            return dfs(root)[1]
        return 0
```