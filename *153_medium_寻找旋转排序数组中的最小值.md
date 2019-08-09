# Leetcode 153 寻找旋转排序数组中的最小值
***
### 题目描述

假设按照升序排序的数组在预先未知的某个点上进行了旋转。

( 例如，数组 `[0,1,2,4,5,6,7]` 可能变为 `[4,5,6,7,0,1,2]` )。

请找出其中最小的元素。

你可以假设数组中不存在重复元素。


**示例1:**  

	输入: [3,4,5,1,2]
	输出: 1

**示例2:**  

	输入: [4,5,6,7,0,1,2]
	输出: 0


### 考点

二分查找



### 代码
执行用时: **88ms**, 内存消耗: **13.9MB**

```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        
        left, right = 0, len(nums) - 1
        while left < right:
            mid = left + (right - left) // 2
            if nums[mid] < nums[-1]:
                right = mid
            else:
                left = mid + 1
        return nums[left]
```

### 代码(二分套路公式)

```
class Solution:
    def findMin(self, nums: List[int]) -> int:
        self.__class__.__getitem__ = lambda self, m: nums[m] <= nums[-1]
        return nums[bisect.bisect_left(self, True, 0, len(nums))]
```