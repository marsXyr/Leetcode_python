# Leetcode 面试题 57 和为s的两个数字
***
### 题目描述

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

**示例1：**    

	输入：nums = [2,7,11,15], target = 9
	输出：[2,7] 或者 [7,2]
	
**示例2：**    

	输入：nums = [10,26,30,31,47,60], target = 40
	输出：[10,30] 或者 [30,10]


	
**说明：**

* `1 <= nums.length <= 10^5`
* `1 <= nums[i] <= 10^6`


**考点**

双指针


### 代码1
执行用时: **136ms**, 内存消耗: **24.7MB**

```
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        
        left, right = 0, len(nums) - 1
        while left < right:
            if nums[left] + nums[right] < target:
                left += 1
            elif nums[left] + nums[right] > target:
                right -= 1
            else:
                return [nums[left], nums[right]]
```





