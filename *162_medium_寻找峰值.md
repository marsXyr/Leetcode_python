# Leetcode 162 寻找峰值
***
### 题目描述

峰值元素是指其值大于左右相邻值的元素。

给定一个输入数组 `nums`，其中 `nums[i] ≠ nums[i+1]`，找到峰值元素并返回其索引。

数组可能包含多个峰值，在这种情况下，返回任何一个峰值所在位置即可。

你可以假设 `nums[-1] = nums[n] = -∞`。

**示例1:**  

	输入: nums = [1,2,3,1]
	输出: 2
	解释: 3 是峰值元素，你的函数应该返回其索引 2。
	
**示例2:**  

	输入: nums = [1,2,1,3,5,6,4]
	输出: 1 或 5 
	解释: 你的函数可以返回索引 1，其峰值元素为 2；
     	 或者返回索引 5， 其峰值元素为 6。
	
**说明：**你的解法应该是 **O(logN)** 时间复杂度的。

### 考点

二分查找

### 思路
遍历数组时间复杂度`O(N)`不符合题意。因为题目要求时间复杂度满足`O(logN)`所以应该想到二分查找。  
但是并没有明显的规律，需要去思考归纳一下。思考发现，如果:   
`nums[mid] < nums[mid+1]`  则峰值点存在于`mid+1 - right` 中  
`nums[mid] > nums[mid+1]`  则峰值点存在于`left - mid`中       

### 代码
执行用时: **52ms**, 内存消耗: **13MB**。

```
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1
        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] < nums[mid+1]:
                left = mid + 1
            else:
                right = mid
        return left
```





