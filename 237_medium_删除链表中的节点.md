# Leetcode 237 删除链表中的节点
***
### 题目描述
给定一个二叉树，返回它的 *中序* 遍历。


**示例:**  

	输入: [1,null,2,3]
       1
        \
         2
        /
       3

    输出: [1,3,2]

	
**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？

### 考点

* 二叉树


### 代码(递归)
执行用时: **48ms**, 内存消耗: **12.9MB**。


```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def __init__(self):
        self.res = []
    
    def inorder(self, root):
        if root is None:
            return 
        
        self.inorderTraversal(root.left)
        self.res.append(root.val)
        self.inorderTraversal(root.right)
    
    def inorderTraversal(self, root: TreeNode) -> List[int]:
        if root is None:
            return []
        
        self.inorder(root)
        
        return self.res
```

### 代码(迭代)
```
class Solution(object):
    def inorderTraversal(self, root):
        """
        :type root: TreeNode
        :rtype: List[int]
        """
        st1, st2 = list(), list()
        while True :
            while root:
                st1.append(root)
                root = root.left
            if not st1:
                return st2
            root = st1.pop()
            st2.append(root.val)
            root = root.right
```

