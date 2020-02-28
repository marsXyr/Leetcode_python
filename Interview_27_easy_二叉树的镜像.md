# Leetcode 面试题 27 二叉树的镜像
***
### 题目描述

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入:

          4
        /   \
       2     7
      / \   / \
     1   3 6   9
镜像输出：

          4
        /   \
       7     2
      / \   / \
     9   6 3   1
     

**示例1：**    

	输入：root = [4,2,7,1,3,6,9]
	输出：[4,7,2,9,6,3,1]


**说明：**

* `0 <= 节点个数 <= 10000`


**考点**

树


### 代码（递归）
执行用时: **52ms**, 内存消耗: **13.5MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:        
        if not root: return root       
        root.left, root.right = self.mirrorTree(root.right), self.mirrorTree(root.left)
        return root
```

### 代码2（迭代）

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def mirrorTree(self, root: TreeNode) -> TreeNode:
        if not root: return []
        stack = [root]
        while stack:
            nextStack = []
            while stack:
                node = stack.pop(0)
                node.left, node.right = node.right, node.left
                if node.left: nextStack.append(node.left)
                if node.right: nextStack.append(node.right)
            stack = nextStack
        return root
```









