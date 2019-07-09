# Leetcode 938 二叉搜索树的范围和
***
### 题目描述
给定二叉搜索树的根结点 `root`，返回 `L` 和 `R`（含）之间的所有结点的值的和。

二叉搜索树保证具有唯一的值。


**示例1:**

	输入：root = [10,5,15,3,7,null,18], L = 7, R = 15
	输出：32
	
**示例2:**

	输入：root = [10,5,15,3,7,13,18,1,null,6], L = 6, R = 10
	输出：23
	

**说明：**

1. 树中的结点数量最多为 10000 个。
2. 最终的答案保证小于 2^31。



### 考点

树


### 代码
执行用时: **364ms**, 内存消耗: **21.2MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def rangeSumBST(self, root: TreeNode, L: int, R: int) -> int:
        
        def visit(root, nodeList):
            if root:
                nodeList.append(root.val)
            else:
                return
            visit(root.left, nodeList)
            visit(root.right, nodeList)
        
        nodeList = []
        visit(root, nodeList)
        return sum([x for x in nodeList if (x >= L and x <= R) ])
```

### 代码2(执行用时：220ms)

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def rangeSumBST(self, root: TreeNode, L: int, R: int) -> int:
        
       
        if not root:
            return 0
        elif L<=root.val<=R and root:
            return root.val + self.rangeSumBST(root.left, L, R)+self.rangeSumBST(root.right, L, R)
        # 當前節點小於L時，那麼它的左字樹都會小於L
        elif root.val<L:
            return self.rangeSumBST(root.right, L, R)
        # 當前節點的屬性大於R時，那麼它的右節點都會大於R
        else:
            return self.rangeSumBST(root.left, L, R)
```
