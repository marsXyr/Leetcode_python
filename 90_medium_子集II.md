# Leetcode 90 子集II
***
### 题目描述
给定一个可能包含重复元素的整数数组 `nums`，返回该数组所有可能的子集（幂集）。

**说明：**解集不能包含重复的子集。

**示例1：**

	输入: [1,2,2]
	输出:
	[
      [2],
      [1],
      [1,2,2],
      [2,2],
      [1,2],
      []
    ]
	

### 考点

数组、回溯

### 思路

常规回溯思路

### 代码
执行用时: **68ms**, 内存消耗: **13.3MB**

```
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []

        def back(nums, index, part):
            if part not in res:
                res.append(part)
            for i in range(index, len(nums)):
                back(nums, i+1, part + [nums[i]])

        back(nums, 0, [])
        return res
```
