# Leetcode 671 二叉树中第二小的节点
***
### 题目描述
给定一个非空特殊二叉树，每个节点都是正数，并且每个节点的子节点数量只能为`2`或`0`。如果一个节点有两个子节点的话，那么这个节点的值不大于它的子节点的值。  
给出这样的一个二叉树，你需要输出所有节点中的**第二小的值**。如果第二小的值不存在的话，输出-1。  


**示例 1:**   
	
	输入:  
	    2
	   / \
	  2   5
	     / \
	    5   7
	
	输出：5
	说明：最小的值是2，第二小的值是5

**示例 2:**   
	
	输入:  
	    2
	   / \
	  2   2
	
	输出：-1
	说明：最小的值是2，但是不存在第二小的值。
	
 
	
### 关键点  

* 第二小的值，root值存在且是第一小的值。


### 考点

* BFS


### 代码  
执行用时 **52ms**, 内存消耗 **13MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    
    def firstbigger(self, root, val):
        if root is None: return -1
        if root.val > val: return root.val
        min_left = self.firstbigger(root.left, val)
        min_right = self.firstbigger(root.right, val)
        if min_left < 0: return min_right
        if min_right < 0: return min_left
        return min(min_left, min_right)
    
    
    def findSecondMinimumValue(self, root: TreeNode) -> int:
        return self.firstbigger(root, root.val)
```


	
