# Leetcode 653 两树之和IV - 输入 BST
***
### 题目描述
给定一个二叉搜索树和一个目标结果，如果 BST 中存在两个元素且它们的和等于给定的目标结果，则返回 True。

**示例1:**   
	
	输入: 
	    5
   	   / \
  	  3   6
	 / \   \
	2   4   7

	Target = 9

	输出: True
	
**示例2:**   
	
	输入: 
            5
           / \
          3   6
         / \   \
        2   4   7

	Target = 28

	输出: False
	

### 考点

* 二叉搜索树


### 代码  
执行用时: **128ms**, 内存消耗: **15.6MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    
    def __init__(self):
        self.nums = []
    
    def dfs(self, root):
        self.nums.append(root.val)
        if root.left:
            self.dfs(root.left)
        if root.right:
            self.dfs(root.right)
        return;
    
    def findTarget(self, root: TreeNode, k: int) -> bool:
        if (root is None) or (root and root.left is None and root.right is None):
            return False
        self.dfs(root)
        d = dict()
        for x in self.nums:
            if str(x) not in d:
                d[str(x)] = 1
            else:
                d[str(x)] += 1
            if k-x != x:
                if str(k-x) in d:
                    return True
            else:
                if d[str(x)] > 1:
                    return True
        return False
                            
```

### Smart Solution (100ms)
换一种写法

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def findTarget(self, root: TreeNode, k: int) -> bool:
        if not root:
            return False

        queue = [root]
        nums = set()
        for node in queue:
            val = node.val
            if k - val in nums:
                return True
            nums.add(val)

            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

        return False
```







	
