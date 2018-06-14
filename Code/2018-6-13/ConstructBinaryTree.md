# Construct Binary Tree from Preorder and Inorder Traversal

## Description

Given preorder and inorder traversal of a tree, construct the binary tree.

## 思路

这道题主要是和树的结构相关，如果采用前序遍历的话，那么第一个元素一定是root。当使用中序的时候，第一个元素一定是最左的叶子，然后是其父结点，一直到根结点为止。由此，左边的子树可以根据root在中序里的位置找出来，右子树也是同理。基本思路就是不断从preorder中取出root，然后过呢据inorder来构建树。

## 代码

``` python
class Solution:
    def buildTree(self, preorder, inorder):
        """
        :type preorder: List[int]
        :type inorder: List[int]
        :rtype: TreeNode
        """
        if inorder:
            index = inorder.index(preorder.pop(0))
            root = TreeNode(inorder[index])
            root.left = self.buildTree(preorder, inorder[:index])
            root.right = self.buildTree(preorder, inorder[index+1:])
            return root
```