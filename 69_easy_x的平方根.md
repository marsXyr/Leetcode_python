# Leetcode 69 x的平方根
***
### 题目描述

实现 `int sqrt(int x)` 函数。

计算并返回 `x` 的平方根，其中 `x` 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。


**示例1:**

	输入: 4
	输出: 2

**示例2：**

	输入: 8
	输出: 2
	说明: 8 的平方根是 2.82842..., 
	     由于返回类型是整数，小数部分将被舍去。


### 考点

二分查找


### 代码
执行用时: **44ms**, 内存消耗: **13.9MB**

```
class Solution:
    def mySqrt(self, x: int) -> int:
        left, right = 1, x - 1
        while left < right:
            mid = (left + right) // 2
            res = mid ** 2
            if res < x:
                left = mid + 1
            elif res > x:
                right = mid - 1
            else:
                return mid
        return left - 1 if left ** 2 > x else left
```

