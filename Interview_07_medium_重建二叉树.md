# Leetcode 面试题 07 重建二叉树
***
### 题目描述

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

**示例1：**    

例如，给出
	
	前序遍历 preorder = [3,9,20,15,7]
	中序遍历 inorder = [9,3,15,20,7]
	
返回如下的二叉树：

	    3
       / \
      9  20
        /  \
       15   7


	
**说明：**

* `0 <= 节点个数 <= 5000`


**考点**

二叉树


### 代码1
执行用时: **204ms**, 内存消耗: **87.2MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> TreeNode:
        if not preorder: return None
        loc = inorder.index(preorder[0])
        root = TreeNode(preorder[0])
        root.left = self.buildTree(preorder[1:loc+1], inorder[:loc])
        root.right = self.buildTree(preorder[loc+1:], inorder[loc+1:])
        return root     
```







