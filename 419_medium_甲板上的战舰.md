# Leetcode 419 甲板上的战舰
***
### 题目描述

给定一个二维的甲板， 请计算其中有多少艘战舰。 战舰用 `'X'`表示，空位用 `'.'`表示。 你需要遵守以下规则：

* 给你一个有效的甲板，仅由战舰或者空位组成。
* 战舰只能水平或者垂直放置。换句话说,战舰只能由 `1xN` (1 行, N 列)组成，或者 `Nx1` (N 行, 1 列)组成，其中N可以是任意大小。
* 两艘战舰之间至少有一个水平或垂直的空位分隔 - 即没有相邻的战舰。


**示例:**

    X..X
	...X
	...X
	
	在上面的甲板中有2艘战舰。
	
**无效样例：**

	...X
	XXXX
	...X

	你不会收到这样的无效甲板 - 因为战舰之间至少会有一个空位将它们分开。
	
**进阶：**

你可以用**一次扫描算法**，只使用**O(1)额外空间**，并且**不修改**甲板的值来解决这个问题吗？

### 考点

数组


### 思路

只需要判断每个战舰的左上方是否有战舰

### 代码
执行用时: **76ms**, 内存消耗: **14.3MB**

```
class Solution:
    def countBattleships(self, board: List[List[str]]) -> int:
        res = 0
        if not board or not board[0]:
            return 0
        for i in range(len(board)):
            for j in range(len(board[0])):
                if board[i][j] == 'X':
                    if (i > 0 and board[i-1][j] == 'X') or (j > 0 and board[i][j-1] == 'X'):
                        continue
                    else:
                        res += 1
        return res
```

