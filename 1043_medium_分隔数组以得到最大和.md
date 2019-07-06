# Leetcode 1043 分隔数组以得到最大和
***
### 题目描述
给出整数数组 `A`，将该数组分隔为长度最多为 `K` 的几个（连续）子数组。分隔完成后，每个子数组的中的值都会变为该子数组中的最大值。

返回给定数组完成分隔后的最大和。


**示例：**

	输入：A = [1,15,7,9,2,5,10], K = 3
	输出：84
	解释：A 变为 [15,15,15,9,10,10,10]



**注意：**

1. `1 <= K <= A.length <= 500`
2. `0 <= A[i] <= 10^6`


### 考点

动态规划、图


### 思路

用dp数组记录每个位置的最大和，dp[i]表示0...i位置元素的最大和。遍历数组A,对于当前位置，向前看K个位置，得到最大的和。


### 代码
执行用时: **828ms**, 内存消耗: **13.1MB**

```
class Solution:
    def maxSumAfterPartitioning(self, A: List[int], K: int) -> int:
        dp = [0 for _ in range(len(A))]
        for i, x in enumerate(A):
            subAMax = x
            for j in range(1, K + 1):
                if i - (j - 1) >= 0:
                    subAMax = max(subAMax, A[i-(j-1)])
                    if i - j < 0:
                        dp[i] = max(dp[i], subAMax * j)
                    else:
                        dp[i] = max(dp[i], dp[i-j] + subAMax * j)
        return dp[-1]
```

### 代码2(换一种写法，执行用时340ms):

```
class Solution:
    def maxSumAfterPartitioning(self, A: List[int], K: int) -> int:
        n = len(A)
        curmax = 0
        res = [0 for _ in range(n)]
        for i in range(len(A)):
            if i < K:
                curmax = max(A[i], curmax)
                res[i] = curmax*(i+1)
            else:
                curmax = 0
                for j in range(1, K+1):
                    curmax = max(A[i-j+1], curmax)
                    res[i] = max(res[i], res[i-j]+curmax*j)
        return res[n-1]
```
