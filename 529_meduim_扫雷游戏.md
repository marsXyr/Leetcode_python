# Leetcode 529 扫雷游戏
***
### 题目描述
让我们一起来玩扫雷游戏！

给定一个代表游戏板的二维字符矩阵。 **'M'** 代表一个未挖出的地雷，**'E'** 代表一个未挖出的空方块，**'B'** 代表没有相邻（上，下，左，右，和所有4个对角线）地雷的已挖出的空白方块，**数字**（'1' 到 '8'）表示有多少地雷与这块已挖出的方块相邻，**'X'** 则表示一个已挖出的地雷。

现在给出在所有未挖出的方块中（'M'或者'E'）的下一个点击位置（行和列索引），根据以下规则，返回相应位置被点击后对应的面板：

1. 如果一个地雷（'M'）被挖出，游戏就结束了- 把它改为 **'X'**。
2. 如果一个**没有相邻地雷**的空方块（'E'）被挖出，修改它为（'B'），并且所有和其相邻的方块都应该被递归地揭露。
3. 如果一个**至少与一个地雷相邻**的空方块（'E'）被挖出，修改它为数字（'1'到'8'），表示相邻地雷的数量。
4. 如果在此次点击中，若无更多方块可被揭露，则返回面板。 


**示例1：**   
	
	输入: 

	[['E', 'E', 'E', 'E', 'E'],
 	['E', 'E', 'M', 'E', 'E'],
 	['E', 'E', 'E', 'E', 'E'],
 	['E', 'E', 'E', 'E', 'E']]

	Click : [3,0]

	输出: 

	[['B', '1', 'E', '1', 'B'],
 	['B', '1', 'M', '1', 'B'],
 	['B', '1', '1', '1', 'B'],
 	['B', 'B', 'B', 'B', 'B']]
 	
 	解释：
 <img src="images/529_1.png" width="500" height="300" >

**示例2：**   
	
	输入: 

	[['B', '1', 'E', '1', 'B'],
 	['B', '1', 'M', '1', 'B'],
 	['B', '1', '1', '1', 'B'],
 	['B', 'B', 'B', 'B', 'B']]

	Click : [1,2]

	输出: 

	[['B', '1', 'E', '1', 'B'],
 	['B', '1', 'X', '1', 'B'],
 	['B', '1', '1', '1', 'B'],
 	['B', 'B', 'B', 'B', 'B']]
 	
 	解释：
 <img src="images/529_2.png" width="500" height="300" >
	
    	
**注意：**  

1. 输入矩阵的宽和高的范围为 [1,50]。
2. 点击的位置只能是未被挖出的方块 ('M' 或者 'E')，这也意味着面板至少包含一个可点击的方块。
3. 输入面板不会是游戏结束的状态（即有地雷已被挖出）。
4. 简单起见，未提及的规则在这个问题中可被忽略。例如，当游戏结束时你不需要挖出所有地雷，考虑所有你可能赢得游戏或标记方块的情况。
	

### 考点

* DFS


### 代码  
执行用时: **208ms**, 内存消耗: **17.2MB** 

```
class Solution:
    
    def checkBound(self, x, y, row, col):
        if x < 0 or x >= row or y < 0 or y >= col:
            return False
        else:
            return True
    
    def count(self, board, x, y):
        cnt = 0
        row, col = len(board), len(board[0])
        neighbour = [[x-1, y], [x+1, y], [x, y-1], [x, y+1], [x-1, y-1], [x-1, y+1], [x+1, y-1], [x+1, y+1]]
        for block in neighbour:
            if self.checkBound(block[0], block[1], row, col):
                if board[block[0]][block[1]] == 'M':
                    cnt += 1
        return cnt
    
    def dfs(self, board, x, y):
        row, col = len(board), len(board[0])
        neighbour = [[x-1, y], [x+1, y], [x, y-1], [x, y+1], [x-1, y-1], [x-1, y+1], [x+1, y-1], [x+1, y+1]]
        for block in neighbour:
            if self.checkBound(block[0], block[1], row, col):
                if board[block[0]][block[1]] == 'E':
                    cnt = self.count(board, block[0], block[1])
                    if cnt == 0:
                        board[block[0]][block[1]] = 'B'
                        self.dfs(board, block[0], block[1])
                    else:
                        board[block[0]][block[1]] = str(cnt)
    
    def updateBoard(self, board: List[List[str]], click: List[int]) -> List[List[str]]:
        if board[click[0]][click[1]] == 'M':
            board[click[0]][click[1]] = 'X'
            return board
        x, y, row, col = click[0], click[1], len(board), len(board[0])
        cnt = self.count(board, x, y)
        if cnt > 0:
            board[x][y] = str(cnt)
            return board
        board[x][y] = 'B'
        self.dfs(board, x, y)
        return board
```









	
