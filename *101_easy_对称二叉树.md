# Leetcode 101 对称二叉树
***
### 题目描述

给定一个二叉树，检查它是否是镜像对称的。

例如，二叉树 `[1,2,2,3,4,4,3]` 是对称的。
**示例1:**  

	    1
       / \
      2   2
     / \ / \
    3  4 4  3
    
但是下面这个 `[1,2,2,null,3,null,3]` 则不是镜像对称的:

        1
       / \
      2   2
       \   \
       3    3


**说明：**  分别用递归和迭代两种方法解决这个问题。

### 考点

树、DFS/BFS


### 代码(递归)
执行用时: **84ms**, 内存消耗: **14MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        
        def isMirror(p, q):
            if not p and not q:
                return True
            if not p or not q:
                return False
            if p.val != q.val:
                return False
            return isMirror(p.left, q.right) and isMirror(p.right, q.left)
        
        return isMirror(root, root)
```

### 代码(迭代, 执行用时：60ms)

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        
        stack = [root]
        while stack:
            val = []
            nexStack = []
            for node in stack:
                if not node:
                    val.append(None)
                    continue
                val.append(node.val)
                nexStack.append(node.left)
                nexStack.append(node.right)
            if val != val[::-1]:
                return False
            stack = nexStack
        return True
```