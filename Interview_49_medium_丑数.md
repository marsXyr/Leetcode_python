# Leetcode 面试题 49 丑数
***
### 题目描述

我们把只包含因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。


**示例1：**

	输入: n = 10
	输出: 12
	解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。	
	

**说明：**

* `1 是丑数。`
* `n 不超过1690。`


**考点**

三指针、动态规划


### 代码
执行用时: **252ms**, 内存消耗: **13.5MB**

```
class Solution:
    def nthUglyNumber(self, n: int) -> int:
        p2, p3, p5 = 0, 0, 0
        dp = [0] * n
        dp[0] = 1
        for i in range(1, n):
            dp[i] = min(dp[p2] * 2, min(dp[p3] * 3, dp[p5] * 5))
            if dp[i] == dp[p2] * 2: p2 += 1
            if dp[i] == dp[p3] * 3: p3 += 1
            if dp[i] == dp[p5] * 5: p5 += 1
        return dp[-1]
```



