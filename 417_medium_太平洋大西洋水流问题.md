# Leetcode 417 太平洋大西洋水流问题
***
### 题目描述
给定一个 `m x n` 的非负整数矩阵来表示一片大陆上各个单元格的高度。“太平洋”处于大陆的左边界和上边界，而“大西洋”处于大陆的右边界和下边界。  
规定水流只能按照上、下、左、右四个方向流动，且只能从高到低或者在同等高度上流动。  
请找出那些水流可以流动到“太平洋”，又能流动到“大西洋”的陆地单元的坐标。  

**提示:** 

	1. 输出坐标的顺序不重要
	2. m 和 n 都小于150

**示例:**   
	
	给定下面的 5x5 矩阵:  
	  
	   	太平洋 ~ ~ ~ ~ ~ ~ ~
	   	    ~ 1  2  2  3 (5) *
	   	    ~ 3  2  3 (4)(4) *
	   	    ~ 2  4 (5) 3  1  * 
	   	    ~(6)(7) 1  4  5  *
	   	    ~(5) 1  1  2  4  *
			   * * * * * * * 大西洋
	
	返回:
	
	[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (上图中带括号的单元). 
	
### 关键点  

* 讨论matrix是否为空
* 从上边界的所有点向四周高地搜索，标记可达太平洋的高地(水是从高处到达低处,逆向相反)
* 从左边界的所有点向四周高地搜索，标记可达太平洋的高地
* 从下边界的所有点向四周高地搜索，标记可达大西洋的高地
* 从右边界的所有点向四周高地搜索，标记可达大西洋的高地
* 遍历矩阵，找出所有可同时到达太平洋和大西洋的点。


### 考点

* DFS


### 代码  
执行用时 **252ms**, 内存消耗 **14MB**

```
class Solution:
    
    def dfs(self, matrix, array, row, column):
        if (row < 0) or (row >= self.m) or (column < 0) or (column >= self.n) or array[row][column]:
            return
        
        # 标记
        array[row][column] = 1 
        
        # 向四个方向搜索
        if(row - 1 >= 0) and (matrix[row - 1][column] >= matrix[row][column]):
            self.dfs(matrix, array, row - 1, column)
        if(row + 1 < self.m) and (matrix[row + 1][column] >= matrix[row][column]):
            self.dfs(matrix, array, row + 1, column)
        if(column - 1 >= 0) and (matrix[row][column - 1] >= matrix[row][column]):
            self.dfs(matrix, array, row, column - 1)
        if(column + 1 < self.n) and (matrix[row][column + 1] >= matrix[row][column]):
            self.dfs(matrix, array, row, column + 1)
    
    
    
    def pacificAtlantic(self, matrix: List[List[int]]) -> List[List[int]]:
        
        if (len(matrix) == 0) or (len(matrix[0]) == 0):
            return []
        self.m, self.n = len(matrix), len(matrix[0])
        Pacific = [[0 for x in range(self.n)] for y in range(self.m)]
        Atlantic = [[0 for x in range(self.n)] for y in range(self.m)]
        ret = []
        
        for i in range(self.m):
            self.dfs(matrix, Pacific, i, 0)
            self.dfs(matrix, Atlantic, i, self.n - 1)
        for j in range(self.n):
            self.dfs(matrix, Pacific, 0, j)
            self.dfs(matrix, Atlantic, self.m - 1, j)
        
        for i in range(self.m):
            for j in range(self.n):
                if (Pacific[i][j] == 1) and (Atlantic[i][j] == 1):
                    ret.append([i, j])
        
        return ret
```


	