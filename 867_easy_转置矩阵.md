# Leetcode 867 转置矩阵
***
### 题目描述
给定一个矩阵 `A`， 返回 `A` 的转置矩阵。

矩阵的转置是指将矩阵的主对角线翻转，交换矩阵的行索引与列索引。


**示例1:**   

	输入：[[1,2,3],[4,5,6],[7,8,9]]
	输出：[[1,4,7],[2,5,8],[3,6,9]]
	
**示例2:**

	输入：[[1,2,3],[4,5,6]]
	输出：[[1,4],[2,5],[3,6]]
	
**示例3:**

1. `1 <= A.length <= 1000`
2. `1 <= A[0].length <= 1000`


### 考点

数组


### 代码
执行用时: **76ms**, 内存消耗: **14.5MB**

```
class Solution:
    def transpose(self, A: List[List[int]]) -> List[List[int]]:
        m, n = len(A), len(A[0])
        res = [[0] * m for _ in range(n)]
        for i in range(m):
            for j in range(n):
                res[j][i] = A[i][j]
        return res
```

### 代码(简洁写法)

```
class Solution:
    def transpose(self, A: List[List[int]]) -> List[List[int]]:
        return list(zip(*A))
```
