# Leetcode 面试题 54 二叉搜索树的第k大节点

***
### 题目描述

给定一棵二叉搜索树，请找出其中第k大的节点。


**示例1：**

	输入: root = [3,1,4,null,2], k = 1
	   3
	  / \
	 1   4
	  \
	   2
	输出: 4
	
	
**示例2：**

	输入: root = [5,3,6,2,4,null,null,1], k = 3
	       5
	      / \
	     3   6
	    / \
	   2   4
	  /
	 1
	输出: 4


**说明：**

* `1 ≤ k ≤ 二叉搜索树元素个数`


**考点**

树

### 代码
执行用时: **52ms**, 内存消耗: **17.8MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def kthLargest(self, root: TreeNode, k: int) -> int:
        self.nums = []
        def inorder(root):
            if not root: return 
            if len(self.nums) >= k: return
            inorder(root.right)
            self.nums.append(root.val)
            inorder(root.left)
        inorder(root)
        return self.nums[k-1]
```



