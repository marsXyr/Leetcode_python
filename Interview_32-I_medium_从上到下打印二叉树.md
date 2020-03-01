# Leetcode 面试题 32-I 从上到下打印二叉树
***
### 题目描述

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

         3
        / \
       9  20
         /  \
        15   7
返回：

	[3,9,20,15,7]


**说明：**

* `节点总数 <= 1000`


**考点**

树


### 代码
执行用时: **44ms**, 内存消耗: **13.7MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[int]:
        if not root: return []
        queue, res = [root], []
        while queue:
            node = queue.pop(0)
            res.append(node.val)
            if node.left: queue.append(node.left)
            if node.right: queue.append(node.right)
        return res
```








