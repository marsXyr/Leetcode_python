# Leetcode 501 二叉搜索树中的众数
***
### 题目描述
给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

* 结点左子树中所含结点的值小于等于当前结点的值
* 结点右子树中所含结点的值大于等于当前结点的值
* 左子树和右子树都是二叉搜索树

例如：
给定 BST `[1,null,2,2]`,

	  1
      \
       2
      /
     2
	
`返回[2]`.
	
**提示:** 如果众数超过1个，不需考虑输出顺序

**进阶:** 你可以不使用额外的空间吗？（假设由递归产生的隐式调用栈的开销不被计算在内）



### 考点

树

### 思路

二叉搜索树的中序遍历结果是一个从小到大排序好的数组。然后再求数组中的众数。


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
    def findMode(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        treeList = []
        
        def inorder(root):
            if root.left:
                inorder(root.left)
            treeList.append(root.val)
            if root.right:
                inorder(root.right)
        inorder(root)
        
        preVal, curCount, maxCount = treeList[0], 1, 1
        res = []
        for curVal in treeList[1:]:
            if preVal == curVal:
                curCount += 1
            else:
                if curCount > maxCount:
                    res.clear()
                    res.append(preVal)
                    maxCount = curCount
                    curCount = 1
                elif curCount == maxCount:
                    res.append(preVal)
                    curCount = 1
                else:
                    curCount = 1
            preVal = curVal
        if curCount > maxCount:
            res.clear()
            res.append(preVal)
        elif curCount == maxCount:
            res.append(preVal)
        
        return res
```

### 代码2(进阶, 执行时间：64ms)

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def findMode(self, root: TreeNode) -> List[int]:
        self.maxn = 1
        self.curn = 1
        self.nums = []
        self.pre = None
        self.inOrder(root)
        
        return self.nums
    
    def inOrder(self, root):
        if root == None:
            return None
        self.inOrder(root.left)
        if self.pre:
            if root.val == self.pre.val:
                self.curn += 1
            else:
                self.curn = 1
        
        
        if self.curn > self.maxn:
            self.nums = []
            self.nums.append(root.val)
            self.maxn = self.curn
        elif self.curn == self.maxn:
            self.nums.append(root.val)
        self.pre = root
        
        self.inOrder(root.right)
```