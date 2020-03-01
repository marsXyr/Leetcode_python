# Leetcode 面试题 29 顺时针打印矩阵
***
### 题目描述

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。
     
**示例1：**    

	输入：matrix = [[1,2,3],[4,5,6],[7,8,9]]
	输出：[1,2,3,6,9,8,7,4,5]
	
**示例2：**

	输入：matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
	输出：[1,2,3,4,8,12,11,10,9,5,6,7]


**说明：**

* `0 <= matrix.length <= 100`
* `0 <= matrix[i].length <= 100`


**考点**

数组


### 代码
执行用时: **56ms**, 内存消耗: **13.8MB**

```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        res = []
        while matrix:
            res += matrix.pop(0)
            matrix = list(zip(*matrix))[::-1]
        return res
```








