# Leetcode 144 二叉树的前序遍历
***
### 题目描述
给定一个二叉树，返回它的 *前序* 遍历。


**示例:**

	输入: [1,null,2,3]  
       1
        \
         2
        /
       3 

    输出: [1,2,3]
	
**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？



### 考点

树


### 代码1(递归)
执行用时: **48ms**, 内存消耗: **13MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        if root is None:
            return []
        return [root.val] + preorderTraversal(root.left) + preorderTraversal(root.right)
```

### 代码2(迭代, 执行时间：48ms)

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def preorderTraversal(self, root: TreeNode) -> List[int]:
        if root is None:
            return []
        stack = [root]
        res = []
        while stack:
            cur = stack.pop()
            res.append(cur.val)
            if cur.right:
                stack.append(cur.right)
            if cur.left:
                stack.append(cur.left)
        return res
```