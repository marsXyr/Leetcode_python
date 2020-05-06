# Leetcode 41 缺失的第一个正数

***
### 题目描述

给你一个未排序的整数数组，请你找出其中没有出现的最小的正整数。

**示例1：**

	输入: [1,2,0]
	输出: 3

**示例2：**

```
输入: [3,4,-1,1]
输出: 2
```

**示例3：**

```
输入: [7,8,9,11,12]
输出: 1
```

**注意**

你的算法的时间复杂度应为O(*n*)，并且只能使用常数级别的额外空间。

**考点**

数组

### 代码

执行用时: **40ms**, 内存消耗: **13.5MB**

```
class Solution:
    def firstMissingPositive(self, nums: List[int]) -> int:
        if 0 not in nums: nums.append(0)
        for i in range(len(nums)):
            if nums[i] == i: continue
            while 0 <= nums[i] < len(nums) and nums[i] != i and nums[i] != nums[nums[i]]:
                nums[nums[i]], nums[i] = nums[i], nums[nums[i]]
        for i in range(1, len(nums)):
            if nums[i] != i: return i
        return len(nums)
```



