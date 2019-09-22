# Leetcode 563 二叉树的坡度
***
### 题目描述

给定一个二叉树，计算**整个树**的坡度。

一个树的**节点的坡度**定义即为，该节点左子树的结点之和和右子树结点之和的**差的绝对值**。空结点的的坡度是0。

**整个树**的坡度就是其所有节点的坡度之和。


**示例:**

	输入: 
         1
       /   \
      2     3
	输出: 1
	解释: 
	结点的坡度 2 : 0
	结点的坡度 3 : 0
	结点的坡度 1 : |2-3| = 1
	树的坡度 : 0 + 0 + 1 = 1


**注意：**

1. 任何子树的结点的和不会超过32位整数的范围。
2. 坡度的值不会超过32位整数的范围。

### 考点

树


### 代码
执行用时: **708ms**, 内存消耗: **15.9MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    
    def __init__(self):
        self.res = 0
        
    def nodeSum(self, root):
        if not root: return 0
        return root.val + self.nodeSum(root.left) + self.nodeSum(root.right)           
    
    def findTilt(self, root: TreeNode) -> int:
        if not root: return 0
        return abs(self.nodeSum(root.left) - self.nodeSum(root.right)) + self.findTilt(root.left) + self.findTilt(root.right)
```

### 代码2(保存中间结果)

```
# Definition for a binary tree node.
# class TreeNode:
#      def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def __init__(self):
        self.sum = 0
    def findTilt(self, root: TreeNode) -> int:
        def dp(root):
            if not root:
                return 0
            left = root.left.val + dp(root.left) if root.left else 0
            right = root.right.val + dp(root.right) if root.right else 0
            self.sum += abs(left-right)
            return left+right
        dp(root)
        return self.sum
```