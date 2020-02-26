# Leetcode 面试题 33 二叉搜索树的后序遍历序列
***
### 题目描述

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。


参考以下这颗二叉搜索树：

        5
       / \
      2   6
     / \
    1   3

**示例1：**    

	输入: [1,6,3,2,5]
	输出: false
	
**示例2：**    

	输入: [1,3,2,6,5]
	输出: true


	
**说明：**

* `数组长度 <= 1000`


### 考点

树、递归

### 思路

**思路1：** 单调栈。   
二叉搜索树满足: left < root < right，后序遍历的顺序是: left -> right -> root, 后序遍历的逆序是: root -> right -> left 亦为换了一个方向的前序遍历，反向遍历数组即可。

因为往右子树遍历的过程中，val 是越来越大的，一旦出现 val 小于栈顶元素时，说明开始进入左子树 (二叉搜索树的定义)。但是这个左子树是从哪个节点开始的呢？

单调栈帮我们记录了这些节点，只要栈顶元素比当前节点大，就表示还是右子树，要移除，因为我们要找到这个左孩子节点直接连接的父节点，也就是找到这个子树的根，只要栈顶元素还大于当前节点，就要一直弹出，直到栈顶元素小于节点，或者栈为空。栈顶的上一个元素就是子树节点的根。

接下来，数组继续往前遍历，之后的左子树的每个节点，都要比子树的根要小，才能满足二叉搜索树。

总的时间复杂度为O(n)。因为每个节点都只会进栈一次和出栈一次，虽然看上去有两个循环，其实是O(2*N)的复杂度，去掉常数就是O(N)了。空间复杂很好看出来，一样O(N)。

**思路2：** 递归。

最后一个数为根节点，通过根节点不断切割左右子树，递归判断左右子树是否为二叉搜索树。


### 代码1（单调栈）
执行用时: **36ms**, 内存消耗: **13.5MB**

```
class Solution:
    def verifyPostorder(self, postorder: List[int]) -> bool:
        stack = []
        prevElem = float('inf')
        for node in postorder[::-1]:
            if node > prevElem:
                return False
            while stack and node < stack[-1]:
                prevElem = stack.pop()
            stack.append(node)
        return True
```

### 代码2（递归）
```
class Solution:
    def verifyPostorder(self, postorder: List[int]) -> bool:
        
        def helper(nums):
            if len(nums) <= 1: return True
            root = nums[-1]
            for i in range(len(nums)):
                if nums[i] > root: break
            for j in range(i, len(nums)-1):
                if nums[j] < root: return False
            return helper(nums[:i]) and helper(nums[i:-1])
        
        if not postorder: return True
        return helper(postorder)
```




