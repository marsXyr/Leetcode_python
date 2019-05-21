# Leetcode 572 另一个树的子树
***
### 题目描述
给定两个非空二叉树 **s** 和 **t**，检验 **s** 中是否包含和 **t** 具有相同结构和节点值的子树。**s** 的一个子树包括 **s** 的一个节点和这个节点的所有子孙。**s** 也可以看做它自身的一棵子树。


**示例1:**  

	给定的树 s:

         3
        / \
       4   5
      / \
     1   2
    
    给定的树 t：
    
       4 
      / \
     1   2
    
    返回 true，因为 t 与 s 的一个子树拥有相同的结构和节点值。
    

**示例2:**  

	给定的树 s：

         3
        / \
       4   5
      / \
     1   2
        /
       0
       
    给定的树 t：

       4
      / \
     1   2
    
    返回 false。


### 考点

* 树+递归

### 思路
对 s 中的每个节点都跟 t 进行比较。

### 代码1
执行用时: **292ms**, 内存消耗: **14.5MB**。

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSubtree(self, s: TreeNode, t: TreeNode) -> bool:
        def dfs(s):
            if s is None: return False
            if isEqual(s, t) is False:
                return dfs(s.left) or dfs(s.right)
            return True
        def isEqual(s, t):
            if s is None and t is None:
                return True
            if s is None or t is None:
                return False
            if s.val != t.val:
                return False
            return isEqual(s.left, t.left) and isEqual(s.right, t.right)
        return dfs(s)
```

        
### 代码2（执行用时：88ms）


```
class Solution:
    def isSubtree(self, s: 'TreeNode', t: 'TreeNode') -> 'bool':
        def dfs(a, b):
            if not a or not b:
                return not a and not b

            if a.val == b.val and dfs(a.left, b.left) and dfs(a.right, b.right):
                return True

            if b is t:
                return dfs(a.left, t) or dfs(a.right, t)

            return dfs(a, t)

        return dfs(s, t)     
```
