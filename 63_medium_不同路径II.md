# Leetcode 63 不同路径II
***
### 题目描述

一个机器人位于一个 *m x n* 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

<img src="images/63.png" width='400' height='200'>

网格中的障碍物和空位置分别用 `1` 和 `0` 来表示。

**说明：** *m* 和 *n* 的值均不超过 100。

**示例:**

	输入:
    [
        [0,0,0],
        [0,1,0],
        [0,0,0]
	]
	输出: 2
	解释:
	3x3 网格的正中间有一个障碍物。
	从左上角到右下角一共有 2 条不同的路径：
	1. 向右 -> 向右 -> 向下 -> 向下
	2. 向下 -> 向下 -> 向右 -> 向右



### 考点

动态规划


### 代码
执行用时: **72ms**, 内存消耗: **13.8MB**

```
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not len(obstacleGrid) or not len(obstacleGrid[0]):
            return 0       
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        dp = [[0] * n for _ in range(m)]
        dp[0][0] = 1 
        for i in range(m):
            for j in range(n):
                if obstacleGrid[i][j] == 1:
                    dp[i][j] = 0
                else:
                    if i >= 1 and dp[i-1][j] != 0:
                        dp[i][j] += dp[i-1][j]
                    if j >= 1 and dp[i][j-1] != 0:
                        dp[i][j] += dp[i][j-1]
        return dp[m-1][n-1]
```


