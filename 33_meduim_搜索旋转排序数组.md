# Leetcode 33 搜索旋转排序数组
***
### 题目描述
假设按照升序排序的数组在预先未知的某个点上进行了旋转。    

（例如，数组`[0,1,2,4,5,6,7]`可能变为`[4,5,6,7,0,1,2]`）。  

搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回`-1`。  

你可以假设数组中不存在重复元素。  

你的算法时间复杂度必须是`O(log n)`级别。

**示例1:**   
	
	输入: nums = [4,5,6,7,0,1,2], target = 0
	输出: 4
	
**示例2:**   
	
	输入: nums = [4,5,6,7,0,1,2], target = 3
	输出: -1
	

### 考点

* 递归+二分查找

### 思路
递归将数组一分为二，其中一个一定是有序的，另一个可能有序可能无序。如果`nums[first]`小于`nums[mid]`则`[first:mid+1]`部分有序，否则另一部分有序。判断完后，如果`target`值在有序部分中，则用二分法查找，如果不在有序部分中，则递归将另一部分一分为二。。。

### 代码  
执行用时: **52ms**, 内存消耗: **13.3MB**

```
class Solution:
    
    def binarySearch(self, nums, first, last, target):
        while first <= last:
            mid = (first + last) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                first = mid + 1
            else:
                last = mid - 1
        return -1
    
    def helper(self, nums, first, last, target):
        if first <= last:
            mid = (first + last) // 2
            if nums[first] <= nums[mid]:
                if nums[first] <= target <= nums[mid]:
                    idx = self.binarySearch(nums, first, mid, target)
                    if idx >= 0:
                        return idx
                else:
                    return self.helper(nums, mid + 1, last, target)
            else:
                if nums[mid] <= target <= nums[last]:
                    idx = self.binarySearch(nums, mid, last, target)
                    if idx >= 0:
                        return idx
                else:
                    return self.helper(nums, first, mid-1, target)
        return -1
    
    def search(self, nums: List[int], target: int) -> int:
        return self.helper(nums, 0, len(nums) - 1, target)
              
```

### Smart Solution (36ms)
好的吧 - -

```
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        if not nums:
            return -1

        low, high = 0, len(nums) - 1

        while low <= high:
            mid = (low + high) >> 1
            if target == nums[mid]:
                return mid

            if nums[low] <= nums[mid]:
                if nums[low] <= target <= nums[mid]:
                    high = mid - 1
                else:
                    low = mid + 1
            else:
                if nums[mid] <= target <= nums[high]:
                    low = mid + 1
                else:
                    high = mid - 1

        return -1
```







	