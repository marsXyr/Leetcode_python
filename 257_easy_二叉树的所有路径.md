# Leetcode 257 二叉树的所有路径
***
### 题目描述
给定一个二叉树，返回所有从根节点到叶子节点的路径。  

**说明：**  叶子节点是指没有子节点的节点。


**示例:**

	输入:

       1
     /   \
    2     3
     \
      5

    输出: ["1->2->5", "1->3"]

    解释: 所有根节点到叶子节点的路径为: 1->2->5, 1->3


### 考点

* 树+DFS

### 思路   
DFS遍历


### 代码
执行用时: **56ms**, 内存消耗: **13MB**。


```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        if root is None:
            return []
        res = []
        return self.dfs(root, "", res)
    
    def dfs(self, root, path, res):
        if root.left is None and root.right is None:
            path = path + "->" + str(root.val)
            res.append(path[2:])
            return res
        path = path + "->" + str(root.val)
        if root.left:            
            self.dfs(root.left, path, res)
        if root.right:
            self.dfs(root.right, path, res)
        return res
```
