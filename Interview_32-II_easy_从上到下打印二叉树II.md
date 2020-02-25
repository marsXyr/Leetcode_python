# Leetcode 面试题 32-II 从上到下打印二叉树II
***
### 题目描述

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

**示例1：**    

	给定二叉树: [3,9,20,null,null,15,7],
	    3
       / \
      9  20
        /  \
       15   7
    返回其层次遍历结果：
    [
    [3],
    [9,20],
    [15,7]
    ]


	
**说明：**

* `节点总数 <= 1000`


### 考点

树


### 代码
执行用时: **56ms**, 内存消耗: **13.5MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        if not root: return []
        res = []
        stack = [root]
        while stack:
            next_stack = []
            vals = []
            while stack:
                cur_node = stack.pop(0)
                vals.append(cur_node.val)
                if cur_node.left: next_stack.append(cur_node.left)
                if cur_node.right: next_stack.append(cur_node.right)
            res.append(vals)
            stack = next_stack
        return res
```



