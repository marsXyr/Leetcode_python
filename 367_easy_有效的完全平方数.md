# Leetcode 367 有效的完全平方数
***
### 题目描述

给定一个正整数 num，编写一个函数，如果 num 是一个完全平方数，则返回 True，否则返回 False。

**说明：** 不要使用任何内置的库函数，如  `sqrt`。

**示例1:**  

	输入：16
	输出：True
	
	
**示例2:**

	输入：14
	输出：False


### 考点

二分查找


### 代码
执行用时: **36ms**, 内存消耗: **13.8MB**

```
class Solution:
    def isPerfectSquare(self, num: int) -> bool:
        left, right = 0, num
        while left <= right:
            mid = (left + right) // 2
            if mid ** 2 < num:
                left = mid + 1
            elif mid ** 2 > num:
                right = mid - 1
            else:
                return True
        return False
```

