# Leetcode 118 杨辉三角
***
### 题目描述

给定一个非负整数 *numRows*，生成杨辉三角的前 *numRows* 行。

<img src="images/118.gif" width="200" height="200" >

在杨辉三角中，每个数是它左上方和右上方的数的和。

**示例：**

	输入: 5
	输出:
	[
         [1],
        [1,1],
       [1,2,1],
      [1,3,3,1],
     [1,4,6,4,1]
	]


### 考点

数组


### 代码
执行用时: **44ms**, 内存消耗: **12.9MB**。

```
class Solution:
    def generate(self, numRows: int) -> List[List[int]]:
        res = [[1] * l for l in range(1, numRows + 1)]
        for i in range(2, numRows):
            for j in range(1, i):
                res[i][j] = res[i-1][j-1] + res[i-1][j]
        return res
```




