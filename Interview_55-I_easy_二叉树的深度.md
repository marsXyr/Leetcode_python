# Leetcode 面试题 55-I 二叉树的深度
***
### 题目描述

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

**示例1:**    

	 给定二叉树 [3,9,20,null,null,15,7]，
	     3
        / \
       9  20
         /  \
        15   7
     返回它的最大深度 3 。
	

	
**说明：**

* `节点总数 <= 10000`


### 考点

树


### 代码
执行用时: **52ms**, 内存消耗: **15MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def maxDepth(self, root: TreeNode) -> int:
        if not root: return 0
        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
```


