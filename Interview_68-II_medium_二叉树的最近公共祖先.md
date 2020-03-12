# Leetcode 面试题 68-II 二叉树的最近公共祖先

***
### 题目描述

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]


<img src="images/Interview_68-II.png" width="200" height="200">

**示例1：**

	输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
	输出: 3
	解释: 节点 5 和节点 1 的最近公共祖先是节点 3。



**示例2：**

	输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
	输出: 5
	解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。

**说明：**

* `所有节点的值都是唯一的。`
* `p、q 为不同节点且均存在于给定的二叉树中。`


**考点**

树、递归


### 代码
执行用时: **140ms**, 内存消耗: **23.7MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        if not root or root == p or root == q: return root
        left = self.lowestCommonAncestor(root.left, p, q)
        right = self.lowestCommonAncestor(root.right, p, q)
        if not left: return right
        if not right: return left
        return root
```

### 代码2

```
class Solution:
    def lowestCommonAncestor(self, root: TreeNode, p: TreeNode, q: TreeNode) -> TreeNode:
        
        ppath, qpath = [], []
        def dfs(root, node, path):
            if not root: return False
            path.append(root)      
            if root.val == node.val: return True
            if dfs(root.left, node, path) or dfs(root.right, node, path): return True          
            path.pop()
        
        dfs(root, p, ppath)
        dfs(root, q, qpath)
        
        i = 0
        while i < len(ppath) and i < len(qpath) and ppath[i] == qpath[i]:
            res = ppath[i]
            i += 1
        return res
```




