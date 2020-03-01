# Leetcode 面试题 32-III 从上到下打印二叉树III
***
### 题目描述

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

         3
        / \
       9  20
         /  \
        15   7
返回其层次遍历结果：

       [
         [3],
         [20,9],
         [15,7]
       ]


**说明：**

* `节点总数 <= 1000`


**考点**

树


### 代码
执行用时: **56ms**, 内存消耗: **13.7MB**

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
        cur_level, res = [root], []
        i = 0
        while cur_level:
            next_level, vals = [], []
            while cur_level:
                node = cur_level.pop(0)
                vals.append(node.val)
                if node.left: next_level.append(node.left)
                if node.right: next_level.append(node.right)
            if i % 2 == 0:
                res.append(vals)
            else:
                res.append(vals[::-1])
            cur_level = next_level
            i += 1
        return res
```








