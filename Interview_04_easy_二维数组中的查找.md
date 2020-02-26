# Leetcode 面试题 04 二维数组中的查找
***
### 题目描述

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

**示例1：**    

	[
    [1,   4,  7, 11, 15],
    [2,   5,  8, 12, 19],
    [3,   6,  9, 16, 22],
    [10, 13, 14, 17, 24],
    [18, 21, 23, 26, 30]
    ]
    
给定 target = `5`，返回 `true`。

给定 target = `20`，返回 `false`。


	
**说明：**

* `0 <= n <= 1000`

* `0 <= m <= 1000`


**考点**

二分查找

**思路**

1. 对行列分别使用二分查找，时间复杂度 O(logm*logn)
2. 找规律


### 代码1
执行用时: **44ms**, 内存消耗: **17.4MB**

```
class Solution:
    
    # 二分搜索
    def binarySearch(self, array, target, left, right):      
        while left <= right:           
            mid = left + (right - left) // 2            
            if array[mid] < target:
                left = mid + 1
            elif array[mid] > target:
                right = mid - 1
            else:
                return mid
        return left + (right - left) // 2
    
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        
        # 递归函数
        def helper(matrix, target, leftX, rightX, leftY, rightY):
            if leftX > rightX or leftY > rightY: return False
            # 找出中间行
            mid = leftX + (rightX - leftX) // 2
            # 对该行应用二分搜索，找出中间列
            res = self.binarySearch(matrix[mid], target, leftY, rightY)
            if matrix[mid][res] == target: return True
            # 该值的左上部分都比target小，弃之。右下部分都比该值大，弃之。递归剩余两部分
            return helper(matrix, target, mid+1, rightX, leftY, res) or helper(matrix, target, leftX, mid-1, res+1, rightY)
        
        # 处理特殊情况
        if not matrix or len(matrix) == 0 or len(matrix[0]) == 0: return False
        m, n = len(matrix) - 1, len(matrix[0]) - 1
        if matrix[0][0] > target or matrix[m][n] < target: return False
        # 进入递归
        return helper(matrix, target, 0, m, 0, n)        
```

### 代码2
```
class Solution:
    
    def findNumberIn2DArray(self, matrix: List[List[int]], target: int) -> bool:
        
        # 处理特殊情况
        if not matrix or len(matrix) == 0 or len(matrix[0]) == 0: return False
        m, n = len(matrix) - 1, len(matrix[0]) - 1
        if matrix[0][0] > target or matrix[m][n] < target: return False

        x, y = 0, n
        while x <= m and y >= 0:
            if matrix[x][y] < target: x += 1
            elif matrix[x][y] > target: y -=1
            else: return True
        return False
```





