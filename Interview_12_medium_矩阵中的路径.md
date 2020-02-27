# Leetcode 面试题 12 矩阵中的路径
***
### 题目描述

请设计一个函数，用来判断在一个矩阵中是否存在一条包含某字符串所有字符的路径。路径可以从矩阵中的任意一格开始，每一步可以在矩阵中向左、右、上、下移动一格。如果一条路径经过了矩阵的某一格，那么该路径不能再次进入该格子。例如，在下面的3×4的矩阵中包含一条字符串“bfce”的路径（路径中的字母用加粗标出）。

[["a","**b**","c","e"],
["s","**f**","**c**","s"],
["a","d","**e**","e"]]

但矩阵中不包含字符串“abfb”的路径，因为字符串的第一个字符b占据了矩阵中的第一行第二个格子之后，路径不能再次进入这个格子。


**示例1：**    

	输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
	输出：true
	
**示例2：**

	输入：board = [["a","b"],["c","d"]], word = "abcd"
	输出：false

**说明：**

* `1 <= board.length <= 200`
* `1 <= board[i].length <= 200`


**考点**

动态规划，回溯


### 代码
执行用时: **212ms**, 内存消耗: **14.7MB**

```
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        m, n = len(board), len(board[0])       
        visited = [[0] * n for _ in range(m)]
        
        def dfs(kth, i, j):
            if kth == len(word): return True
            res = False
            if 0 <= i < m and 0 <= j < n and board[i][j] == word[kth] and not visited[i][j]:
                visited[i][j] = 1
                res = dfs(kth+1, i+1, j) or dfs(kth+1, i-1, j) or dfs(kth+1, i, j+1) or dfs(kth+1, i, j-1)
                if not res: visited[i][j] = 0
            return res
        
        for i in range(m):
            for j in range(n):
                if dfs(0, i, j): return True
        return False 
```







