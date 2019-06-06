# Leetcode 120 三角形最小路径和
***
### 题目描述

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

例如，给定三角形：

	[
     [2],
    [3,4],
    [6,5,7],
    [4,1,8,3]
    ]
	
自顶向下的最小路径和为 `11`（即，**2 + 3 + 5 + 1** = 11）。


**说明：**

如果你可以只使用 O(n) 的额外空间（n 为三角形的总行数）来解决这个问题，那么你的算法会很加分。

### 考点

动态规划

### 思路
回溯法想一下，时间复杂度太高，可能会超出时间限制。所以还是考虑动态规划。  
这道题用动态规划求解，思路还是很直接的：从下往上遍历，求得本层的元素值加上下一层相邻元素值中较小者。  
方程为：`triangle[i][j] += min(triangle[i+1][j], triangle[i+1][j+1])`  而最顶层元素就是最短路径的值。


### 代码
执行用时: **56ms**, 内存消耗: **13.4MB**。

```
class Solution:
    def minimumTotal(self, triangle: List[List[int]]) -> int:
        if len(triangle) == 0:
            return 0
        for i in range(len(triangle)-2, -1, -1):
            for j in range(len(triangle[i])):
                triangle[i][j] += min(triangle[i+1][j], triangle[i+1][j+1])
                
        return triangle[0][0]
```





