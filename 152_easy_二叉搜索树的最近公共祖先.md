# Leetcode 152 二叉搜索树的最近公共祖先
***
### 题目描述
给定一个二叉搜索树，找到该树中两个指定节点的最近公共祖先。  

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个节点 p、q, 最近公共祖先表示为一个节点 x, 满足 x 是 p、q 的祖先且 x 的深度尽可能大(**一个节点也可以是它自己的祖先**)。”  

例如，给定如下二叉搜索树: root = [6,2,9,0,7,9,null,null,3,5]     

![GitHub](https://github.com/marsXyr/Leetcode_python/tree/master/images/235.png)

**示例1:**   
	
	输入: root = [6,2,9,0,7,9,null,null,3,5], p = 2, q = 8  
	输出: 6  
	解释: 节点 2 和节点 8 的最近公共祖先是 6。

**示例2:**   
	
	输入: root = [6,2,9,0,7,9,null,null,3,5], p = 2, q = 4  
	输出: 2  
	解释: 节点 2 和节点 4的最近公共祖先是 2，因为根据定义最近公共祖先节点可以为节点本身。
	
**说明:**  

* 所有节点的值都是唯一的。
* p、q为不同节点且均存在于给定的二叉搜索树中。 

### 考点

* 递归、二叉搜索树


### 思路 
根据p、q的值与每次递归时root的值比较，如果p和q的值都小于root的值则向左子树递归，都大于则向右子树递归，如果一个小于一个大于，则说明最近公共祖先必为本次递归的root，直接返回。 

### 代码  
执行用时 **104ms**, 内存消耗 **13.4MB**

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if root == None:
            return None
        if (p.val < root.val) and (q.val < root.val):
            return self.lowestCommonAncestor(root.left, p, q)
        elif (p.val > root.val) and (q.val > root.val):
            return self.lowestCommonAncestor(root.right, p ,q)
        else:
            return root              
```

### Smart Solution

其实思路一样，只是把递归调用函数过程改成了while循环，速度就变快了。

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
class Solution:
    def lowestCommonAncestor(self, root, p, q):
        """
        :type root: TreeNode
        :type p: TreeNode
        :type q: TreeNode
        :rtype: TreeNode
        """
        a, b = (p, q) if p.val < q.val else (q, p)
        cur = root
        while cur:
            if cur is a or cur is b or (a.val < cur.val < b.val):
                return cur
            cur = cur.right if a.val > cur.val else cur.left
```




	