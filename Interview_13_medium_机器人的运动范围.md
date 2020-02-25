# Leetcode 面试题 13 机器人的运动范围
***
### 题目描述

地上有一个m行n列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0]` 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？


**示例1：**    

	输入：m = 2, n = 3, k = 1
	输出：3
	
**示例2：**    

	输入：m = 3, n = 1, k = 0
	输出：1


	
**说明：**

* `1 <= n,m <= 100`
* `0 <= k <= 20`


### 考点

DFS


### 代码
执行用时: **88ms**, 内存消耗: **17MB**

```
class Solution:
    def movingCount(self, m: int, n: int, k: int) -> int:
        
        def helper(i, j):
            sum = 0
            while i:
                sum += i % 10
                i //= 10
            while j >= 1:
                sum += j % 10
                j //= 10
            return sum   
        visited = [[0] * n for _ in range(m)]
        def dfs(i, j):
            if i < 0 or j < 0 or i >= m or j >= n or visited[i][j] == 1 or helper(i, j) > k: return 0                 
            visited[i][j] = 1
            return dfs(i, j+1) + dfs(i-1, j) + dfs(i, j-1) + dfs(i+1, j) + 1
    
        return dfs(0, 0)
```



