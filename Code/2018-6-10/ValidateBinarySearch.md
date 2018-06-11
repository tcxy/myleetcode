# Validate Binary Search Tree

## Description

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

   1. The left subtree of a node contains only nodes with keys less than the node's key.
   2. The right subtree of a node contains only nodes with keys greater than the node's key.
   3. Both the left and right subtrees must also be binary search trees.

## 思路

其实就是不断地判断就行了。

## 代码

``` python
class Solution:
    def isValidBST(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        return self.validate(root)
    
    def validate(self, root, less = float('-inf'), great=float('inf')):
        if root:
            if root.val > less and root.val < great:
                return self.validate(root.left, less, root.val) and self.validate(root.right, root.val, great)
            else:
                return False
        return True
```