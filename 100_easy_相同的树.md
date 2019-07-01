# Leetcode 100 相同的树
***
### 题目描述
给定两个二叉树，编写一个函数来检验它们是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。


**示例1：**

	输入:       1         1
                / \       / \
                 2   3     2   3

                [1,2,3],   [1,2,3]

	输出: true
	
**示例2：**

	输入:      1          1
               /           \
                2             2

               [1,2],     [1,null,2]

	输出: false

**示例3:**

	输入:       1         1
                / \       / \
                 2   1     1   2

                [1,2,1],   [1,1,2]

	输出: false



### 考点

树、DFS


### 代码
执行用时: **52ms**, 内存消耗: **12.9MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if not p and not q:
            return True
        if p and q and p.val == q.val:
            return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
        else:
            return False
```

### 代码(执行用时：32ms)

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if p and q:
            return p.val == q.val and self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)
        return p is q
```
