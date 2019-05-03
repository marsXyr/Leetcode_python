# Leetcode 912 排序数组
***
### 题目描述
给定一个整数数组 `nums`，将该数组升序排列。


**示例1:**

	输入：[5,2,3,1]
	输出：[1,2,3,5]
	
**示例2:**

	输入：[5,1,1,2,0,0]
	输出：[0,0,1,1,2,5]
	
**提示:**  

1. `1 <= A.length <= 10000`
2. `-50000 <= A[i] <= 50000`


### 考点

* 数组排序


### 代码
执行用时: **144ms**, 内存消耗: **19.6MB**。


```
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        nums = sorted(nums)
        return nums         
```

### 