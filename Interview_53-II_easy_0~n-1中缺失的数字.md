# Leetcode 面试题 53-II 0~n-1中缺失的数字

***
### 题目描述

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。


**示例1：**

	输入: [0,1,3]
	输出: 2
	
	
**示例2：**

	输入: [0,1,2,3,4,5,6,7,9]
	输出: 8


**说明：**

* `1 <= 数组长度 <= 10000`


**考点**

二分查找

### 代码
执行用时: **64ms**, 内存消耗: **14.4MB**

```
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] != mid: right = mid - 1
            else: left = mid + 1
        return left
```

### 代码2
```
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        return len(nums) * (len(nums)+1) // 2  - sum(nums)
```



