# Leetcode 1014 最佳观光组合
***
### 题目描述
给定正整数数组 `A`，`A[i]` 表示第 `i` 个观光景点的评分，并且两个景点 `i` 和 `j` 之间的距离为 `j - i`。

一对景点（`i < j`）组成的观光组合的得分为（`A[i] + A[j] + i - j`）：景点的评分之和减去它们两者之间的距离。

返回一对观光景点能取得的最高分。


**示例:**

	输入：[8,1,5,2,6]
	输出：11
	解释：i = 0, j = 2, A[i] + A[j] + i - j = 8 + 5 + 0 - 2 = 11
	
**提示:**

1. 	2 <= A.length <= 50000
2. 	1 <= A[i] <= 1000



### 考点

数组


### 思路
采用贪心思路，将问题分解为：`A[i]+ i` 和 `A[j] - j` 的最大值(`i < j`)，我们只需要在遍历 `j` 的时候不断更新 `A[i] + i` 的最大值即可。


### 代码
执行用时: **212ms**, 内存消耗: **16.3MB**

```
class Solution:
    def maxScoreSightseeingPair(self, A: List[int]) -> int:
        res = 0
        pre_max = A[0]
        A[0] = 0
        for j, Aj in enumerate(A):
            res = max(pre_max + Aj - j, res)
            pre_max = max(pre_max, Aj + j)
        return res
```