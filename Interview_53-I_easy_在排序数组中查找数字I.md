# Leetcode 面试题 53-I 在排序数组中查找数字I
***
### 题目描述

统计一个数字在排序数组中出现的次数。

**示例1：**

	输入: nums = [5,7,7,8,8,10], target = 8
	输出: 2
	
	
**示例2：**

	输入: nums = [5,7,7,8,8,10], target = 6
	输出: 0


**说明：**

* `0 <= 数组长度 <= 50000`


**考点**

二分查找

### 代码
执行用时: **28ms**, 内存消耗: **14.5MB**

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums or target > nums[-1] or target < nums[0]: return 0
        left, right = 0, len(nums) - 1
        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] < target:
                left = mid + 1
            elif nums[mid] > target:
                right = mid - 1
            else:
                break
        count = 0
        for i in range(left, right+1, 1):
            if nums[i] == target: count += 1
        return count
```

### 代码2
```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        return bisect.bisect(nums, target) - bisect.bisect_left(nums, target)
```




