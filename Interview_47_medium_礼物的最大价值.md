# Leetcode 面试题 47 礼物的最大价值
***
### 题目描述

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

 
**示例1：**

	输入: 
	[
	  [1,3,1],
	  [1,5,1],
	  [4,2,1]
	]
	输出: 12
	解释: 路径 1→3→5→2→1 可以拿到最多价值的礼物
	
	

**说明：**

* `0 < grid.length <= 200`
* `0 < grid[0].length <= 200`


**考点**

动态规划


### 代码
执行用时: **68ms**, 内存消耗: **14.9MB**

```
class Solution:
    def maxValue(self, grid: List[List[int]]) -> int:
        m, n = len(grid), len(grid[0])
        for i in range(1, m):
            grid[i][0] += grid[i-1][0]
        for i in range(1, n):
            grid[0][i] += grid[0][i-1]
        
        for i in range(1, m):
            for j in range(1, n):
                grid[i][j] += max(grid[i][j-1], grid[i-1][j])
        return grid[m-1][n-1]
```






