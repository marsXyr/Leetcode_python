# Leetcode 441 排列硬币
***
### 题目描述

你总共有 *n* 枚硬币，你需要将它们摆成一个阶梯形状，第 *k* 行就必须正好有 *k* 枚硬币。

给定一个数字 *n*，找出可形成完整阶梯行的总行数。

*n* 是一个非负整数，并且在32位有符号整型的范围内。

**示例1:**

	n = 5

	硬币可排列成以下几行:
	¤
	¤ ¤
	¤ ¤

	因为第三行不完整，所以返回2.
	
**示例2:**

	n = 8

	硬币可排列成以下几行:
	¤
	¤ ¤
	¤ ¤ ¤
	¤ ¤

	因为第四行不完整，所以返回3.


### 考点

二分查找



### 代码1
执行用时: **60ms**, 内存消耗: **14MB**

```
class Solution:
    def arrangeCoins(self, n: int) -> int:
        left, right = 1, n
        while left <= right:
            mid = (left + right) // 2
            sum = mid * (mid + 1) // 2
            if sum < n:
                left = mid + 1
            elif sum > n:
                right = mid - 1
            else:
                return mid
        return left - 1
```

### 代码2

```
class Solution:
    def arrangeCoins(self, n: int) -> int:
        sum = 0
        while n > sum:
            sum += 1
            n -= sum
        return sum
```

