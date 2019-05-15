# Leetcode 199 二叉树的右视图
***
### 题目描述
给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。


**示例:**  

	输入: [1,2,3,null,5,null,4]
	输出: [1, 3, 4]
	解释:

       1            <---
     /   \
    2     3         <---
     \     \
      5     4       <---

	

### 考点

* BFS

### 思路  
BFS，当前层节点保存在 cur 中，下一层节点保存在 nex 中，cur 第一次 pop 出的节点就是最右边的节点，其他的节点判断是否有左右子节点，若有就加入到 nex 中，如果 cur 中节点遍历结束，就 cur = nex, nex = []，进行下一次循环。
循环终止条件是，最后一层全是空, 也就是 cur 长度为0


### 代码
执行用时: **40ms**, 内存消耗: **12.8MB**。


```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        if root is None:
            return []
        res = []
        cur = []
        nex = []
        cur.append(root)
        flag = 1
        while len(cur) > 0:
            node = cur.pop()
            if flag == 1:              
                res.append(node.val)
                flag = 0
            
            if node.right is not None:
                nex = [node.right] + nex
            if node.left is not None:
                nex = [node.left] + nex
            if len(cur) == 0:
                cur = nex
                nex = []
                flag = 1
        return res
```
