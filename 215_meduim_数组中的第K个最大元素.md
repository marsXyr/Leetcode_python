# Leetcode 215 数组中的第K个最大元素
***
### 题目描述
在未排序的数组中找到第 **k** 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。


**示例1:**

	输入: [3,2,1,5,6,4] 和 k = 2
	输出: 5
	
**示例2:**

	输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
	输出: 4
	
**说明:**  

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。


### 考点

* 数组第K大元素


### 代码
执行用时: **144ms**, 内存消耗: **19.6MB**。


```
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        nums = sorted(nums, reverse=True)
        return nums[k-1]       
```
