# Leetcode 59 螺旋矩阵 II
***
### 题目描述
给定一个正整数 n, 生成一个包含 1 到 n^2, 且元素按顺时针顺序螺旋排列的正方形矩阵。

**示例:**   
	
	输入: 3
	输出: [
	       [1, 2, 3],
	       [8, 9, 4],
	       [7, 6, 5]
	      ]  

### 考点

* 二维数组


### 思路 
先求出共需要螺旋赋值(一周)的次数，然后每次循环中，依次右下左上进行赋值，count表示当前矩阵位置需要赋的值 

### 代码  
执行用时 **52ms**, 内存消耗 **13.1MB**

```
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix = [[0 for _ in range(n)] for _ in range(n)]
        iters = int(n // 2) if n % 2 == 0 else int(n // 2 + 1)
        it = 0
        count = 1
        while it < iters:
            for j in range(it, n - it, 1):
                matrix[it][j] = count
                count += 1
            for i in range(it + 1, n - it, 1):
                matrix[i][n-it-1] = count
                count += 1
            for j in range(n - it - 2, it, -1):
                matrix[n-it-1][j] = count
                count += 1
            for i in range(n - it - 1, it, -1):
                matrix[i][it] = count
                count += 1
            it += 1
        return matrix              
```





	
