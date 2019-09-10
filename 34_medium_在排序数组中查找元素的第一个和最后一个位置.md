# Leetcode 34 在排序数组中查找元素的第一个和最后一个位置
***
### 题目描述

给定一个按照升序排列的整数数组 `nums`，和一个目标值 `target`。找出给定目标值在数组中的开始位置和结束位置。

你的算法时间复杂度必须是 `O(log n)` 级别。

如果数组中不存在目标值，返回 `[-1, -1]`。


**示例1:**

	输入: nums = [5,7,7,8,8,10], target = 8
	输出: [3,4]
	
**示例2:**

	输入: nums = [5,7,7,8,8,10], target = 6
	输出: [-1,-1]


### 考点

二分查找


### 代码
执行用时: **128ms**, 内存消耗: **15MB**

```
class Solution:
    def searchRange(self, nums: List[int], target: int) -> List[int]:
        if not nums: return [-1, -1]
        left, right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] < target:
                left = mid + 1
            else:
                right = mid
        if nums[left] != target: return [-1, -1]
        begin, end = left, len(nums)
        while begin < end:
            mid = (begin + end) // 2
            if nums[mid] > target:
                end = mid
            else:
                begin = mid + 1
        return [left, begin-1]
```


