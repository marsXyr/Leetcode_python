# Leetcode 面试题 42 连续子数组的最大和
***
### 题目描述

输入一个整型数组，数组里有正数也有负数。数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

**示例：**

	输入: nums = [-2,1,-3,4,-1,2,1,-5,4]
	输出: 6
	解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。


**说明：**

* `1 <= arr.length <= 10^5`
* `-100 <= arr[i] <= 100`


**考点**

贪心算法、动态规划


### 代码1（贪心算法）
执行用时: **104ms**, 内存消耗: **17.8MB**

```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        res = nums[0]
        for i in range(1, len(nums)):
            nums[i] += max(0, nums[i-1])
            res = max(res, nums[i])
        return res
```

### 代码2（动态规划）
执行用时: **68ms**, 内存消耗: **15MB**

```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:       
        res = nums[0]
        for i in range(1, len(nums)):
            if nums[i-1] > 0:
                nums[i] += nums[i-1]
            res = max(res, nums[i])
        return res
```







