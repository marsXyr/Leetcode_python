# Leetcode 面试题 04.12 求和路径
***
### 题目描述

给定一棵二叉树，其中每个节点都含有一个整数数值(该值或正或负)。设计一个算法，打印节点数值总和等于某个给定值的所有路径的数量。注意，路径不一定非得从二叉树的根节点或叶节点开始或结束，但是其方向必须向下(只能从父节点指向子节点方向)。


**示例1:**    
给定如下二叉树，以及目标和 sum = 22，
	
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
返回:

	3	
	解释：和为 22 的路径有：[5,4,11,2], [5,8,4,5], [4,11,7]


**提示：**

* `节点总数 <= 10000`


### 考点

树、DFS

### 思路




### 代码
执行用时: **168ms**, 内存消耗: **43MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> int:        
        def f(r, s):
            if r:
                s = [i + r.val for i in s] + [r.val]
                return s.count(sum) + f(r.left, s) + f(r.right, s)
            return 0
        return f(root, []) 
```



