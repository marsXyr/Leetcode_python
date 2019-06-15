# Leetcode 119 杨辉三角II
***
### 题目描述

给定一个非负索引 k，其中 k ≤ 33，返回杨辉三角的第 k 行。

<img src="images/119.gif" width="200" height="200" >

**示例：**

	输入: 3
	输出: [1,3,3,1]

**进阶：**

你可以优化你的算法到 O(k) 空间复杂度吗？

### 考点

数组


### 代码
执行用时: **40ms**, 内存消耗: **12.8MB**。

```
class Solution:
    def getRow(self, rowIndex: int) -> List[int]:
        if rowIndex == 0:
            return [1]
        if rowIndex == 1:
            return [1, 1]
        cur = [1, 1]
        nex = []
        for _ in range(1, rowIndex):
            nex = [1]
            for i in range(1, len(cur)):
                nex.append(cur[i-1] + cur[i])
            nex.append(1)
            cur = nex
        return cur
```

### 代码
```
class Solution(object):
    def getRow(self, rowIndex):
        row = [1]
        for _ in range(rowIndex):
            row = [x + y for x, y in zip([0]+row, row+[0])]
        return row
```




