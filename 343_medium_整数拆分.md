# Leetcode 343 整数拆分
***
### 题目描述

给定一个正整数 `n`，将其拆分为**至少**两个正整数的和，并使这些整数的乘积最大化。 返回你可以获得的最大乘积。

**示例1:**

	输入: 2
	输出: 1
	解释: 2 = 1 + 1, 1 × 1 = 1。


**示例2：**

	输入: 10
	输出: 36
	解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。
	
**说明: **

* 可以假设 `n` 不小于2且不大于58.


### 考点

动态规划


### 代码
执行用时: **32ms**, 内存消耗: **13MB**

```
import math
class Solution:
    def integerBreak(self, n: int) -> int:
        dp = [1] * (n + 1)
        for i in range(2, n + 1):
            for j in range(1, math.ceil(i / 2) + 1):
                dp[i] = max(dp[i], j * max(dp[i-j], i-j))
        return dp[n]
```



