# Leetcode 437 路径总和 III
***
### 题目描述

给定一个二叉树，它的每个结点都存放着一个整数值。

找出路径和等于给定数值的路径总数。

路径不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

二叉树不超过1000个节点，且节点数值范围是 [-1000000,1000000] 的整数。


**示例:**

    root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

          10
         /  \
        5   -3
       / \    \
      3   2   11
     / \   \
    3  -2   1

    返回 3。和等于 8 的路径有:

    1.  5 -> 3
    2.  5 -> 2 -> 1
    3.  -3 -> 11


### 考点

树


### 思路

想啥呢，暴力递归就完事了。

### 代码
执行用时: **820ms**, 内存消耗: **14.9MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    
    def __init__(self):
        self.res = 0
    
    def pathSum(self, root: TreeNode, sum: int) -> int:
        if not root: return 0
        self.helper(root, 0, sum)
        if root.left: self.pathSum(root.left, sum)
        if root.right: self.pathSum(root.right, sum)
        return self.res
                 
    def helper(self, root, cur, sum):
        if root.val + cur == sum: self.res += 1
        if root.left: self.helper(root.left, cur + root.val, sum)
        if root.right: self.helper(root.right, cur + root.val, sum)
```

