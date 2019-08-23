# Leetcode 107 二叉树的层次遍历II
***
### 题目描述

给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

例如：  
给定二叉树 `[3,9,20,null,null,15,7]`,

        3
       / \
      9  20
        /  \
       15   7
       
返回其自底向上的层次遍历为：

	[
      [15,7],
      [9,20],
      [3]
    ]


### 考点

树、BFS


### 代码
执行用时: **48ms**, 内存消耗: **13.8MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrderBottom(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        stack = [root]
        res = []
        while stack:
            nexStack = []
            val = []
            while stack:
                node = stack.pop(0)
                val.append(node.val)
                if node.left: nexStack.append(node.left)
                if node.right: nexStack.append(node.right)
            res = [val] + res
            stack = nexStack
        return res
```
