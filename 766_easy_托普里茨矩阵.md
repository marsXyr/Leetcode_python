# Leetcode 766 托普里茨矩阵
***
### 题目描述

如果一个矩阵的每一方向由左上到右下的对角线上具有相同元素，那么这个矩阵是托普利茨矩阵。

给定一个 `M x N` 的矩阵，当且仅当它是托普利茨矩阵时返回 `True`。


**示例1:**

    输入: 
	matrix = [
	    [1,2,3,4],
	    [5,1,2,3],
	    [9,5,1,2]
    ]
	输出: True
	解释:
	在上述矩阵中, 其对角线为:
	"[9]", "[5, 5]", "[1, 1, 1]", "[2, 2, 2]", "[3, 3]", "[4]"。
	各条对角线上的所有元素均相同, 因此答案是True。


**示例2:**

	输入:
	matrix = [
      [1,2],
      [2,2]
    ]
    输出: False
	解释: 
	对角线"[1, 2]"上的元素不同。


	
**说明：**

1. `matrix` 是一个包含整数的二维数组。
2. `matrix` 的行数和列数均在 `[1, 20]`范围内。
3. `matrix[i][j]` 包含的整数在 `[0, 99]`范围内。

**进阶：**

1. 如果矩阵存储在磁盘上，并且磁盘内存是有限的，因此一次最多只能将一行矩阵加载到内存中，该怎么办？
2. 如果矩阵太大以至于只能一次将部分行加载到内存中，该怎么办？

### 考点

数组


### 代码
执行用时: **108ms**, 内存消耗: **13.8MB**

```
class Solution:
    def isToeplitzMatrix(self, matrix: List[List[int]]) -> bool:
        if not len(matrix) or not len(matrix[0]):
            return False
        m, n = len(matrix), len(matrix[0])
        for i in range(len(matrix)):
            num = matrix[i][0]
            p, q = i+1, 1
            while p < m and q < n:
                if matrix[p][q] != num:
                    return False
                p, q = p+1, q+1
        for i in range(1, len(matrix[0])):
            num = matrix[0][i]
            p, q = 1, i+1
            while p < m and q < n:
                if matrix[p][q] != num:
                    return False
                p, q = p+1, q+1
        return True
```

### 代码2

只需判断：前行中除最后一个元素外剩余的元素完全等于后行中除第一个元素外剩余的元素。

```
class Solution:
    def isToeplitzMatrix(self, matrix: List[List[int]]) -> bool:
        col_len = len(matrix) 
        row_len = len(matrix[0])
        for i in range(len(matrix) - 1):
            if matrix[i][:-1] != matrix[i + 1][1:]:
                return False
        return True
```