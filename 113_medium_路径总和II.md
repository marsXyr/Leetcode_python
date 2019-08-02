# Leetcode 113 路径总和 II
***
### 题目描述
给定一个二叉树和一个目标和，找到所有从根节点到叶子节点路径总和等于给定目标和的路径。

**说明：** 叶子节点是指没有子节点的节点。


**示例:**  
给定如下二叉树，以及目标和 sum = 22，
	
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

	[
   		[5,4,11,2],
   		[5,8,4,5]
	]



### 考点

DFS、树



### 代码
执行用时: **64ms**, 内存消耗: **19.1MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
        res = []
        if not root:
            return []
        def dfs(root, total, part):
            if root.left is None and root.right is None and root.val + total == sum:
                res.append(part+[root.val])          
            if root.left:
                dfs(root.left, total+root.val, part+[root.val])
            if root.right:
                dfs(root.right, total+root.val, part+[root.val])
        
        dfs(root, 0, [])
        return res
```
