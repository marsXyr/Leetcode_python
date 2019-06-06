# Leetcode 643 子数组最大平均数I
***
### 题目描述

给定 `n` 个整数，找出平均数最大且长度为 `k` 的连续子数组，并输出该最大平均数。

**示例1：**

	输入: [1,12,-5,-6,50,3], k = 4
	输出: 12.75
	解释: 最大平均数 (12-5-6+50)/4 = 51/4 = 12.75


**注意：**

1. 1 <= `k` <= `n` <= 30,000。
2. 所给数据范围 [-10,000，10,000]。

### 考点

数组

### 思路
滑动窗口做法，注意新平均值的计算。

### 代码
执行用时: **184ms**, 内存消耗: **15.3MB**。

```
class Solution:
    def findMaxAverage(self, nums: List[int], k: int) -> float:
        max_avg, cur_avg = sum(nums[:k]) / k, sum(nums[:k]) / k
        for i in range(k, len(nums)):
            cur_avg += (nums[i] - nums[i-k]) / k
            if cur_avg > max_avg:
                max_avg = cur_avg
        return max_avg
```





