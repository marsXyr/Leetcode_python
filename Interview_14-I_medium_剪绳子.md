# Leetcode 面试题 14-I 剪绳子
***
### 题目描述

给你一根长度为 `n` 的绳子，请把绳子剪成整数长度的 `m` 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 `k[0],k[1]...k[m]` 。请问 `k[0]\*k[1]\*...\*k[m]` 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。


**示例1：**    

	输入: 2
	输出: 1
	解释: 2 = 1 + 1, 1 × 1 = 1
	
**示例2：**

	输入: 10
	输出: 36
	解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36

**说明：**

* `2 <= n <= 58`


**考点**

动态规划，找规律


### 代码1（动态规划）
执行用时: **40ms**, 内存消耗: **13.4MB**

```
class Solution:
    def cuttingRope(self, n: int) -> int:

        dp = [0 for i in range(n+1)]
        dp[2] = 1
        for i in range(3, n+1):
            for j in range(i):
                dp[i] = max(dp[i], j * max(i - j, dp[i-j]))
        return dp[n]
```

### 代码2（找规律）

```
class Solution:
    def cuttingRope(self, n: int) -> int:

        if n in [2, 3]: return n - 1        
        res = 1
        while n > 4:
            res *= 3
            n -= 3
        return res * n
```







