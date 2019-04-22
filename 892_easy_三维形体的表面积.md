# Leetcode 892 三维形体的表面积
***
### 题目描述
在 `N * N` 的网格上，我们放置一些 `1 * 1 * 1` 的立方体。  

每个值 `v = grid[i][j]` 表示 `v` 个正方体叠放在单元格 `(i, j)`上。  

返回最终形体的表面积

**示例1:**   
	
	输入：[[2]]
	输出：10
	
**示例2:**   
	
	输入：[[1,2],[3,4]]
	输出：34
	
**示例3:**   
	
	输入：[[1,0],[0,2]]
	输出：16
	
**示例4:**   
	
	输入：[[1,1,1],[1,0,1],[1,1,1]]
	输出：32
	
**示例5:**   
	
	输入：[[2,2,2],[2,1,2],[2,2,2]]
	输出：46

**注意：**

* `1 <= N <= 50`
* `0 <= grid[i][j] <= 50`

### 考点

* 数学

### 思路
先无视是否重合问题，算出表面积，然后减去行和列出现重合的面积。

### 代码  
执行用时: **76ms**, 内存消耗: **13MB**

```
class Solution:
    def surfaceArea(self, grid: List[List[int]]) -> int:
        area = 0
        n = len(grid)
        for i in range(n):
            for j in range(n):
                if grid[i][j]: area += grid[i][j] * 4 + 2
                if i: area -= min(grid[i][j], grid[i-1][j]) * 2
                if j: area -= min(grid[i][j], grid[i][j-1]) * 2
        return area
              
```







	