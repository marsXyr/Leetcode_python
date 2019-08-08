# Leetcode 207 课程表
***
### 题目描述
现在你总共有 n 门课需要选，记为 0 到 n-1。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: [0,1]

给定课程总量以及它们的先决条件，判断是否可能完成所有课程的学习？

**示例1:**  

	输入: 2, [[1,0]] 
	输出: true
	解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。

**示例2:**  

	输入: 2, [[1,0],[0,1]]
	输出: false
	解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。

**说明：**

1. 输入的先决条件是由边缘列表表示的图形，而不是邻接矩阵。
2. 你可以假定输入的先决条件中没有重复的边。


**提示：**

1. 这个问题相当于查找一个循环是否存在于有向图中。如果存在循环，则不存在拓扑排序，因此不可能选取所有课程进行学习。
2. 通过 DFS 进行拓扑排序。
3. 拓扑排序也可以通过 BFS 完成。



### 考点

图、拓扑排序、DFS/BFS


### 思路

**BFS**

1. 统计课程安排图中每个节点的入度，生成 **入度表** `indegrees`。
2. 借助一个队列`queue`，将所有入度为 0 的节点入队。
3. 当`queue`非空时，依次将队首节点出队，在课程安排图中删除此节点`pre`：
	
	* 并不是真正从邻接表中删除此节点`pre`，而是将此节点对应所有邻接节点`cur`的入度 −1 ，即`indegrees[cur] -= 1`。
	* 当入度 −1后邻接节点`cur`的入度为 0，说明`cur`所有的前驱节点已经被“删除”，此时将`cur`入队。
4. 在每次`pre`出队时，执行`numCourses--`；
	* 若整个课程安排图是有向无环图（即可以安排），则所有节点一定都入队/出队过，即完成拓扑排序。若有环，一定有节点的入度始终不为 0。
	* 因此，拓扑排序出队次数等于课程个数，返回`numCourses == 0`判断课程是否可以成功安排。

**DFS**

1. 借助一个标志列表`flags`，用于判断每个节点 `i`（课程）的状态：
	
	1. 未被DFS访问：`i == 0`；
	2. 已被其他节点启动的DFS访问：`i == -1`；
	3. 已被当前节点启动的DFS访问：`i == 1`。
2. 对`numCourses`个节点依次执行DFS，判断每个节点起步DFS是否存在环，若存在环直接返回 False 。DFS流程；
	1. 终止条件：
		* 当`flag[i] == -1`，说明当前访问节点已被其他节点启动的DFS访问，无需再重复搜索，直接返回 True。
		* `当flag[i] == 1`，说明在本轮DFS搜索中节点`i`被第 2 次访问，即课程安排图有环，直接返回 False 。
	2. 将当前访问节点i对应`flag[i]`置 1，即标记其被本轮DFS访问过；
	3. 递归访问当前节点i的所有邻接节点`j`，当发现环直接返回 False ；
	4. 当前节点所有邻接节点已被遍历，并没有发现环，则将当前节点`flag`置为 -1 并返回 True。
3. 若整个图DFS结束并未发现环，返回 True 。



### 代码(BFS)
执行用时: **148ms**, 内存消耗: **15MB**

```
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        
        AList = [[] for _ in range(numCourses)]
        inds = [0 for _ in range(numCourses)]  
        # 建立邻接表以及每个点的入度表
        for cur, pre in prerequisites:
            AList[pre].append(cur)
            inds[cur] += 1
            
        # 选取入度为0的点入队
        queue = []
        for i in range(numCourses):
            if not inds[i]: queue.append(i)
        # 每次从队列中pop出一个点，使该点指向的所有点的入度减1，如果有点入度变为0，则入队
        while queue:
            pre = queue.pop(0)
            # 遍历一个点，课程数减1
            numCourses -= 1
            for cur in AList[pre]:
                inds[cur] -= 1
                if not inds[cur]: queue.append(cur)
        # 如果每个点都遍历一遍且队列为空，则说明无环
        return not numCourses
```

### 代码(DFS)

```
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        def dfs(i, adjacency, flags):
            if flags[i] == -1: return True
            if flags[i] == 1: return False
            flags[i] = 1
            for j in adjacency[i]:
                if not dfs(j, adjacency, flags): return False
            flags[i] = -1
            return True
        
        adjacency = [[] for _ in range(numCourses)]
        flags = [0 for _ in range(numCourses)]
        for cur, pre in prerequisites:
            adjacency[pre].append(cur)
        for i in range(numCourses):
            if not dfs(i, adjacency, flags): return False
        return True
```