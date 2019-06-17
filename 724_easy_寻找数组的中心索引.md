# Leetcode 724 寻找数组的中心索引
***
### 题目描述

给定一个整数类型的数组 `nums`，请编写一个能够返回数组“**中心索引**”的方法。

我们是这样定义数组**中心索引**的：数组中心索引的左侧所有元素相加的和等于右侧所有元素相加的和。

如果数组不存在中心索引，那么我们应该返回 -1。如果数组有多个中心索引，那么我们应该返回最靠近左边的那一个。

**示例1：**

	输入: 
	nums = [1, 7, 3, 6, 5, 6]
	输出: 3
	解释: 
	索引3 (nums[3] = 6) 的左侧数之和(1 + 7 + 3 = 11)，与右侧数之和(5 + 6 = 11)相等。
	同时, 3 也是第一个符合要求的中心索引。

**示例2：**

	输入: 
	nums = [1, 2, 3]
	输出: -1
	解释: 
	数组中不存在满足此条件的中心索引。
	
**说明：**

* `nums` 的长度范围为 `[0, 10000]`。
* 任何一个 `nums[i]` 将会是一个范围在 `[-1000, 1000]` 的整数。

### 考点

数组

### 思路
设置两个数组 `preSum`(从前向后累加)，`lasSum`(从后向前累加)。然后遍历数组，当`preSum[i]==lasSum[i]`时，说明中心索引的位置为`i`。

### 代码
执行用时: **104ms**, 内存消耗: **14.3MB**

```
class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        l = len(nums)
        if l == 0:
            return -1
        preSum, lasSum = [0] * l, [0] * l
        preSum[0], lasSum[0] = nums[0], nums[-1]
        for i in range(1, l):
            preSum[i] = preSum[i-1] + nums[i]
            lasSum[i] = lasSum[i-1] + nums[l-i-1]
        for i in range(l):
            if preSum[i] == lasSum[l-i-1]:
                return i
        return -1
```

### 代码2(执行用时：60ms)

```

class Solution:
    def pivotIndex(self, nums: List[int]) -> int:
        right=sum(nums)
        left=0
        for i in range(len(nums)):
            right-=nums[i]
            if right==left:
                return i
            left+=nums[i]
        return -1
```


