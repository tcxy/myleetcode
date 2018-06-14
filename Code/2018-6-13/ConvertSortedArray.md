# Convert Sorted Array to Binary Search Tree

## Description

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

## 思路

由于数组已经排好序了，其实只要按照数组的中间作为root就行了

## 代码

``` python
class Solution:
    def sortedArrayToBST(self, nums):
        """
        :type nums: List[int]
        :rtype: TreeNode
        """
        if nums:
            length = len(nums)
            index = length // 2
            root = TreeNode(nums[index])
            root.left = self.sortedArrayToBST(nums[:index])
            root.right = self.sortedArrayToBST(nums[index+1:])
            return root
```