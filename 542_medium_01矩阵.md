# Leetcode 542 01矩阵
***
### 题目描述
给定一个由 0 和 1 组成的矩阵，找出每个元素到最近的 0 的距离。

两个相邻元素间的距离为 1 。

**示例1:**  
输入：

	0 0 0
	0 1 0
	0 0 0
输出：  

	0 0 0
	0 1 0
	0 0 0
	
**示例2:**  
输入：

	0 0 0
	0 1 0
	1 1 1
输出：  

	0 0 0
	0 1 0
	1 2 1
	
**注意：**  

* 给定矩阵的元素个数不超过 10000。
* 给定矩阵中至少有一个元素是 0。
* 矩阵中的元素只在四个方向上相邻: 上、下、左、右。

### 考点

* 动态规划/BFS/DFS

### 思路   
先从 左上 遍历,根据左方元素和上方元素得到当前元素的结果，然后右下 遍历，根据右方元素和下方元素得出当前元素最终结果。


### 代码1(动态规划)
执行用时: **628ms**, 内存消耗: **14.9MB**。


```
class Solution:
    def updateMatrix(self, matrix: List[List[int]]) -> List[List[int]]:
        row, col = len(matrix), len(matrix[0])
        for i in range(row):
            for j in range(col):
                if matrix[i][j] == 1:
                    matrix[i][j] = row + col
                if i > 0:
                    matrix[i][j] = min(matrix[i][j], matrix[i-1][j]+1)
                if j > 0:
                    matrix[i][j] = min(matrix[i][j], matrix[i][j-1]+1)
        for i in range(row-1, -1, -1):
            for j in range(col-1, -1, -1):
                
                if i < row - 1:
                    matrix[i][j] = min(matrix[i][j], matrix[i+1][j]+1)
                if j < col - 1:
                    matrix[i][j] = min(matrix[i][j], matrix[i][j+1]+1)
        return matrix
```

### 代码2(BFS, 执行用时:448ms)
```
class Solution(object):
    def updateMatrix(self, matrix):
        if not matrix or not matrix[0]:
            return
        dx = [-1, 0, 1, 0]
        dy = [0, 1, 0, -1]
        
        a = len(matrix)
        b = len(matrix[0])
        def bfs(i, j):
            queue = [(i, j, 0)]

            while queue:
                x, y, dis = queue.pop(0)
                for k in range(4):
                    temp_x = x + dx[k]
                    temp_y = y + dy[k]
                    temp_dis = dis + 1
                    if 0 <= temp_x < a and 0 <= temp_y < b:
                        if matrix[temp_x][temp_y] == 0:
                            return temp_dis
                        queue.append((temp_x, temp_y, temp_dis))

        for i in range(a):
            for j in range(b):
                if matrix[i][j] != 0:
                    matrix[i][j] = bfs(i, j)
        return matrix
```
