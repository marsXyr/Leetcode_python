# Leetcode 222 完全二叉树的节点个数
***
### 题目描述

给出一个**完全二叉树**，求出该树的节点个数。


**说明：**

完全二叉树的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。


**示例:**

	输入: 
        1
       / \
      2   3
     / \  /
    4   5 6

    输出: 6


### 考点

树、二分查找


### 思路

**二分查找**

完全二叉树的高度可以直接通过不断地访问左子树就可以获取    
判断左右子树的高度:     

* 如果相等说明左子树是满二叉树, 然后进一步判断右子树的节点数(最后一层最后出现的节点必然在右子树中)
* 如果不等说明右子树是深度小于左子树的满二叉树, 然后进一步判断左子树的节点数(最后一层最后出现的节点必然在左子树中)

**递归**

很简单 - -


### 代码(二分查找)
执行用时: **104ms**, 内存消耗: **21.5MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def countNodes(self, root: TreeNode) -> int:
        # 判断完全二叉树的深度
        def depth(root):
            level = 0
            while root:
                level += 1
                root = root.left
            return level
        
        if not root:
            return 0
        # 我们只需要判断最后一层节点数量，初始化 res 为前面层所有节点数量
        cur, res = root, int(math.pow(2, depth(root) - 1)) - 1
        while cur:
            # 左右子树高度相同，此时左子树满
            if depth(cur.left) == depth(cur.right):
                # 此时 cur 节点的左右子树都为空，则加上 cur 节点
                if depth(cur.left) == 0:
                    res += 1
                    break
                # 加上最后一层左子树的所有节点
                res += int(math.pow(2, depth(cur.left) - 1))
                cur = cur.right
            # 左右子树高度不同，左子树未满，继续遍历左子树
            else:
                cur = cur.left
        return res
```

### 代码(递归)

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def countNodes(self, root: TreeNode) -> int:
        if not root:
            return 0
        return self.countNodes(root.left) + self.countNodes(root.right) + 1
```