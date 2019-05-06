# Leetcode 934 最短的桥
***
### 题目描述
在给定的二维二进制数组`A`中，存在两座岛。（岛是由四面相连的`1`形成的一个最大组。）  
现在，我们可以将`0`变为`1`，以使两座岛连接起来，变成一座岛。  
返回必须翻转的`0`的最小数目。（可以保证答案至少是1。）


**示例 1:**   
	
	输入: [[0,1],[1,0]]
	输出: 1
	
	   	 
**示例 2:**   
	
	输入: [[0,1,0],[0,0,0],[0,0,1]]
	输出: 2

**示例 2:**   
	
	输入: [[1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1]]
	输出: 1
	
**提示:**   
	
	1. 1 <= A.length = A[0].length <= 100
	2. A[i][j] == 0 或 A[i][j] == 1
	


### 考点

* DFS + BFS

### 解题思路

首先用DFS来确定其中一座岛，把这个岛所有的1变成2(跟另一座岛区分开)。同时需要把这个岛的每个位置都添加到队列中。在找到一座岛后(岛2)，使用BFS，来找到岛2离岛1最近的距离。BFS一步相当于遍历整个队列，把所有走了一步仍是水路的位置设置成2，并放到队列中；如果找到的是岛2，说明这个位置出现过队列中直接continue；如果找到了岛1，直接返回结果。

### 代码  
执行用时 **272ms**, 内存消耗 **16MB**

```
class Solution:

    def dfs(self, A, i, j, visited, queue):
        if visited[i][j]: return
        visited[i][j] = 1
        if A[i][j] == 1:
            queue.append((i, j))
            A[i][j] = 2
            for a in self.act:
                x, y = i + a[0], j + a[1]
                if 0 <= x < self.m and 0 <= y < self.n:
                    self.dfs(A, x, y, visited, queue)

    def shortestBridge(self, A: List[List[int]]) -> int:
        self.m = len(A)
        self.n = len(A[0])
        #        右       下       左       上
        self.act = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        visited = [[0] * self.n for _ in range(self.m)]
        hasfind = False
        queue = collections.deque()

        for i in range(self.m):
            if hasfind: break
            for j in range(self.n):
                if A[i][j] == 1:
                    self.dfs(A, i, j, visited, queue)
                    hasfind = True
                    break
        res = 0
        while queue:
            for _ in range(len(queue)):
                i, j = queue.popleft()
                for a in self.act:
                    x, y = i + a[0], j + a[1]
                    if 0 <= x < self.m and 0 <= y < self.n:
                        visited[x][y] = 1
                        if A[x][y] == 1:
                            return res
                        elif A[x][y] == 0:
                            queue.append((x, y))
                            A[x][y] = 2
                        else:
                            continue
            res += 1

        return -1
```

### Smart Solution

```
import collections


class Solution:
    def shortestBridge(self, A: List[List[int]]) -> int:

        m = len(A)
        visit = set()
        queue = collections.deque()
        newq = collections.deque()

        for k in range(m * m):
            i, j = k // m, k % m
            if A[i][j] == 1:
                visit.add((i, j))
                queue.append((i, j))
                break

        while queue:
            i, j = queue.popleft()
            for x, y in [(i, j + 1), (1 + i, j), (i - 1, j), (i, j - 1)]:
                if 0 <= x < m and 0 <= y < m and (x, y) not in visit:
                    if A[x][y] == 1:
                        visit.add((x, y))
                        queue.append((x, y))
                    elif A[x][y] == 0:
                        newq.append((x, y, 1))

        while newq:
            i, j, step = newq.popleft()
            for x, y in [(i, j + 1), (1 + i, j), (i - 1, j), (i, j - 1)]:
                if 0 <= x < m and 0 <= y < m and (x, y) not in visit:
                    if A[x][y] == 0:
                        visit.add((x, y))
                        newq.append((x, y, step + 1))
                    elif A[x][y] == 1:
                        return step
```


	
