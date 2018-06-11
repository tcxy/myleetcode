# Binary Tree Inorder Traversal

## Description

Given a binary tree, return the inorder traversal of its nodes' values.

```
Input: [1,null,2,3]
   1
    \
     2
    /
   3

Output: [1,3,2]
```

## 思路

这题我比较熟的做法是递归，如何采用iterative的方法我还不大清楚。

## 代码

``` python
class Solution:
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = []
        self.inorder(root,res)
        return res
        
    def inorder(self, root, res):
        if root:
            self.inorder(root.left, res)
            res.append(root.val)
            self.inorder(root.right, res)
```

## iteratively

``` python
class Solution:
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        res = []
        stack = []
        while True:
            while root:
                stack.append(root)
                root = root.left
            if len(stack) == 0:
                return res
            left = stack.pop()
            res.append(left.val)
            root = left.right
```

## 总结

这题我尝试的时候，递归反而快一点。可能主要是因为案例规模的问题。