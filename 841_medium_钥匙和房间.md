# Leetcode 841 钥匙和房间
***
### 题目描述

有 `N` 个房间，开始时你位于 `0` 号房间。每个房间有不同的号码：`0，1，2，...，N-1`，并且房间里可能有一些钥匙能使你进入下一个房间。

在形式上，对于每个房间 `i` 都有一个钥匙列表 `rooms[i]`，每个钥匙 `rooms[i][j]` 由 `[0,1，...，N-1]` 中的一个整数表示，其中 `N = rooms.length`。 钥匙 `rooms[i][j] = v` 可以打开编号为 `v` 的房间。

最初，除 `0` 号房间外的其余所有房间都被锁住。

你可以自由地在房间之间来回走动。

如果能进入每个房间返回 `true`，否则返回 `false`。

**示例1：**

	输入: [[1],[2],[3],[]]
	输出: true
	解释:  
	我们从 0 号房间开始，拿到钥匙 1。
	之后我们去 1 号房间，拿到钥匙 2。
	然后我们去 2 号房间，拿到钥匙 3。
	最后我们去了 3 号房间。
	由于我们能够进入每个房间，我们返回 true。

**示例2：**

	输入：[[1,3],[3,0,1],[2],[0]]
	输出：false
	解释：我们不能进入 2 号房间。

**提示：**  

1. `1 <= rooms.length <= 1000`
2. `0 <= rooms[i].length <= 1000`
3. 所有房间中的钥匙数量总计不超过 `3000`。

### 考点

DFS、图

### 思路
有向图的深度优先搜索。  
设置两个数组`notVisited`、`visited`，分别存放还未遍历过的房间号和已经遍历过的房间号。如果`notVisited`数组为空说明我们已经遍历过所有房间，直接返回，如果当前房间已经遍历过了也直接返回。然后遍历钥匙串中的房间号。

### 代码
执行用时: **92ms**, 内存消耗: **13.9MB**。

```
class Solution:
    def canVisitAllRooms(self, rooms: List[List[int]]) -> bool:
        notVisited = [i for i in range(1, len(rooms))]
        visited = []

        def dfs(curRoom, keys):
            if len(notVisited) == 0:
                return
            if curRoom in visited:
                return
            visited.append(curRoom)
            for key in keys:
                if key in notVisited:
                    notVisited.remove(key)
                dfs(key, rooms[key])

        dfs(0, rooms[0])
        return True if len(notVisited) == 0 else False
```

### 代码2(优化后的，执行用时：40ms)

```
class Solution:
    def canVisitAllRooms(self, rooms: List[List[int]]) -> bool:
        a = set()

        def f(i):
            a.add(i)
            for i in rooms[i]:
                if i not in a:
                    f(i)

        f(0)
        return not (set(range(len(rooms))) - a)
```





