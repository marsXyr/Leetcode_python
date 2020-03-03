# Leetcode 面试题 34 二叉树中和为某一值的路径
***
### 题目描述

输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。

示例:
给定如下二叉树，以及目标和 sum = 22，

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

**说明：**

* `节点总数 <= 10000`


**考点**

回溯


### 代码
执行用时: **52ms**, 内存消耗: **18.7MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:
        self.res = []       
        def back(root, path, curSum, sum):
            if not root: return
            if curSum + root.val == sum and not root.left and not root.right :
                self.res.append(path+[root.val])
            back(root.left, path+[root.val], curSum + root.val, sum)
            back(root.right, path+[root.val], curSum + root.val, sum)       
        back(root, [], 0, sum)
        return self.res
```








