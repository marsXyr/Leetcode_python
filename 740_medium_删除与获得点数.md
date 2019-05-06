# Leetcode 740 删除与获得点数
***
### 题目描述
给定一个整数数组`nums`, 你可以对它进行一些操作。  

每次操作中，选择任意一个`nums[i]`，删除它并获得`nums[i]`的点数，你必须删除**每个**等于`nums[i] - 1`或`nums[i] + 1`的元素。  

开始你拥有0个点数。返回你能通过这些操作获得的最大点数。

**示例1:**   
	
	输入: nums = [3, 4, 2]
	输出: 6
	解释: 
	删除 4 来获得 4 个点数，因此 3 也被删除。
	之后，删除 2 来获得 2 个点数。总共获得 6 个点数
	
**示例2:**   
	
	输入: nums = [2, 2, 3, 3, 3, 4]
	输出: 9
	解释: 
	删除 3 来获得 3 个点数，接着要删除两个 2 和 4 。
	之后，再次删除 3 获得 3 个点数，再次删除 3 获得 3 个点数。
	总共获得 9 个点数。
	

**注意：**

* `nums`的长度最大为`20000`。
* 每个整数`nums[i]`的大小都在`[1, 10000]`范围内。

### 考点

* 动态规划

### 思路
把该问题转化为打劫家舍问题，不能使用相邻的两个数字。动态规划方程为: `dp[i] = max(dp[i-1], dp[i-2] + dp[i])`

### 代码  
执行用时: **56ms**, 内存消耗: **13.2MB**

```
class Solution:  
    def deleteAndEarn(self, nums: List[int]) -> int:
        if not nums or len(nums) == 0:
            return 0
        if len(nums) == 1:
            return nums[0]

        dp = [0] * (max(nums) + 1)

        for x in nums:
            dp[x] += x

        dp[1] = max(dp[0], dp[1])
        for i in range(2, len(dp)):
            dp[i] = max(dp[i - 2] + dp[i], dp[i - 1])

        return dp[-1]
              
```







	
