# Leetcode 面试题 26 树的子结构
***
### 题目描述

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

	     3
        / \
       4   5
      / \
     1   2
给定的树 B：

       4 
      /
     1
     
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。
	

**示例1：**    

	输入：A = [1,2,3], B = [3,1]
	输出：false


**示例2：**

	输入：A = [3,4,5,1,2], B = [4,1]
	输出：true

**说明：**

* `0 <= 节点个数 <= 10000`


**考点**

树


### 代码（递归）
执行用时: **140ms**, 内存消耗: **17.8MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isSubStructure(self, A: TreeNode, B: TreeNode) -> bool:      
        
        def helper(A, B):
            if not B: return True
            return A and A.val == B.val and helper(A.left, B.left) and helper(A.right, B.right)
        
        if not A and not B: return True
        if not A or not B: return False
        if A.val == B.val:
            return helper(A, B) or self.isSubStructure(A.left, B) or self.isSubStructure(A.right, B)
        else: 
            return self.isSubStructure(A.left, B) or self.isSubStructure(A.right, B)
```









