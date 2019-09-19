# Leetcode 230 二叉搜索树中第K小的元素
***
### 题目描述

给定一个二叉搜索树，编写一个函数 `kthSmallest` 来查找其中第 **k** 个最小的元素。


**说明：**  你可以假设 k 总是有效的，1 ≤ k ≤ 二叉搜索树元素个数。 


**示例1:**

	输入: root = [3,1,4,null,2], k = 1
       3
      / \
     1   4
      \
       2
    输出: 1
    
**示例2:**

    输入: root = [5,3,6,2,4,null,null,1], k = 3
	       5
	      / \
	     3   6
	    / \
	   2   4
	  /
	 1
	输出: 3


**进阶：**

如果二叉搜索树经常被修改（插入/删除操作）并且你需要频繁地查找第 k 小的值，你将如何优化 `kthSmallest` 函数？

### 考点

树、二分查找


### 代码1
执行用时: **72ms**, 内存消耗: **18.1MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def kthSmallest(self, root: TreeNode, k: int) -> int:
        node_list = []
        def dfs(root):
            if root.left: dfs(root.left)
            node_list.append(root.val)
            if root.right: dfs(root.right)
        dfs(root)    
        return node_list[k-1]
```

