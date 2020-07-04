# Leetcode 62 不同路径
***
### 题目描述
一个机器人位于一个 *m x n* 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

<img src="images/62.png" width="=400" height="200" >

例如，上图是一个7 x 3 的网格。有多少可能的路径？

**说明：** *m* 和 *n* 的值均不超过 100。

**示例1:**

	输入: m = 3, n = 2
	输出: 3
	解释:
	从左上角开始，总共有 3 条路径可以到达右下角。
	1. 向右 -> 向右 -> 向下
	2. 向右 -> 向下 -> 向右
	3. 向下 -> 向右 -> 向右

	
**示例2:**

	输入: m = 7, n = 3
	输出: 28
	


### 考点

动态规划/数学

### 思路

用数学中的排列组合或动态规划思想都很直接。


### 代码（排列组合）
执行用时: **40ms**, 内存消耗: **13.1MB**

```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        res = 1
        steps = m + n - 2
        div = 1
        for i in range(min(m, n) - 1):
            res *= steps
            div *= i+1
            steps -= 1
        return res // div
```

### 代码2（动态规划, 执行用时：28ms）

```
class Solution:
    def uniquePaths(self, m: int, n: int) -> int:
        if m==1 or n==1:
            return 1
        
        dp = [[0 for i in range(m)] for j in range(n)]
        for i in range(n):
            dp[i][0]=1
        for j in range(m):
            dp[0][j]=1
        
        for i in range(1,n):
            for j in range(1,m):
                dp[i][j] = max(dp[i][j],dp[i-1][j]+dp[i][j-1])
        
        return dp[n-1][m-1]
```
