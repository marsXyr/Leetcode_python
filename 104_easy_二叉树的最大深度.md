# Leetcode 104 二叉树的最大深度
***
### 题目描述
给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明：**  叶子节点是指没有子节点的节点。


**示例1:**   
给定二叉树 `[3,9,20,null,null,15,7]`，

	    3
       / \
      9  20
        /  \
       15   7

返回它的最大深度 3 。


### 考点

树


### 代码
执行用时: **68ms**, 内存消耗: **16.1MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root:
            return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```
