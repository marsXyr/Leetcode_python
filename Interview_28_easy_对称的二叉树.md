# Leetcode 面试题 28 对称的二叉树
***
### 题目描述

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

         1
        / \
       2   2
      / \ / \
     3  4 4  3
     
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

         1
        / \
       2   2
        \   \
        3    3
     

**示例1：**    

	输入：root = [1,2,2,3,4,4,3]
	输出：true
	
**示例2：**

	输入：root = [1,2,2,null,3,null,3]
	输出：false


**说明：**

* `0 <= 节点个数 <= 1000`


**考点**

树


### 代码（递归）
执行用时: **48ms**, 内存消耗: **13.5MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:

        def helper(node1, node2):
            if not node1 and not node2:
                return True
            if not node1 and node2 or node1 and not node2:
                return False
            if node1.val != node2.val:
                return False
            return helper(node1.left, node2.right) and helper(node1.right, node2.left)
        
        return helper(root, root)
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
    def isSymmetric(self, root: TreeNode) -> bool:
 
        if not root: return True
        
        stack = [root]
        while stack:
            next_stack, cur_vals = [], []
            while stack:
                node = stack.pop(0)
                if node.left:
                    cur_vals.append(node.left.val)
                    next_stack.append(node.left)
                else:
                    cur_vals.append(-1)
                if node.right:
                    cur_vals.append(node.right.val)
                    next_stack.append(node.right)
                else:
                    cur_vals.append(-1)
            if cur_vals != cur_vals[::-1]:
                return False
            stack = next_stack
        return True
```









