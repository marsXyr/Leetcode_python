# Leetcode 404 左叶子之和
***
### 题目描述

计算给定二叉树的所有左叶子之和。

**示例1:**

        3
       / \
      9  20
        /  \
       15   7
	
	在这个二叉树中，有两个左叶子，分别是 9 和 15，所以返回 24



### 考点

树


### 代码
执行用时: **52ms**, 内存消耗: **14.3MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:   
    def sumOfLeftLeaves(self, root: TreeNode) -> int:
        if not root:
            return 0
        if root.left and not root.left.left  and not root.left.right:
            return root.left.val + self.sumOfLeftLeaves(root.right)
        else:
            return self.sumOfLeftLeaves(root.left) + self.sumOfLeftLeaves(root.right)
```
