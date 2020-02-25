# Leetcode 面试题 55-II 平衡二叉树
***
### 题目描述

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

**示例1：**    

	给定二叉树 [3,9,20,null,null,15,7]
	    3
       / \
      9  20
        /  \
       15   7
    返回 true 。
	
**示例2：**

	给定二叉树 [1,2,2,3,3,null,null,4,4]
	      1
         / \
        2   2
       / \
      3   3
     / \
    4   4
    返回 false 。

	
**说明：**

* `1 <= 树的结点个数 <= 10000`


### 考点

树


### 代码（从上到下，包含很多重复计算）
执行用时: **64ms**, 内存消耗: **18.3MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        
        def depth(root):
            if not root: return 0
            return 1 + max(depth(root.left), depth(root.right))
        
        if not root: return True
        if abs(depth(root.left) - depth(root.right)) > 1: return False
        return self.isBalanced(root.left) and self.isBalanced(root.right)
```

### 代码 (从下到上，无重复计算)
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isBalanced(self, root: TreeNode) -> bool:

        def depth(root):
            if not root: return 0
            leftDepth = depth(root.left)
            rightDepth = depth(root.right)
            if leftDepth >= 0 and rightDepth >= 0 and abs(leftDepth - rightDepth) <= 1:
                return 1 + max(leftDepth, rightDepth)
            else:
                return -1
        return depth(root) >= 0
```


