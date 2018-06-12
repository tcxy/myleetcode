# Sysmmetric Tree

## Description

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric: 

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

## 思路

这题说白就是树的遍历，相对来说很简单。

## 代码

``` python
class Solution:
    def isSymmetric(self, root):
        """
        :type root: TreeNode
        :rtype: bool
        """
        if not root:
            return True
        return self.compare(root.left, root.right)
    def compare(self, left, right):
        if left == None and right == None:
            return True
        elif left and right:
            if left.val == right.val:
                return self.compare(left.left, right.right) and self.compare(left.right, right.left)
            else:
                return False
        else:
            return False
```