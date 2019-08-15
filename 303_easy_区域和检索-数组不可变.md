# Leetcode 303 区域和检索-数组不可变
***
### 题目描述

给定一个整数数组  *nums*，求出数组从索引 *i* 到 *j  (i ≤ j)* 范围内元素的总和，包含 *i*,  *j* 两点。


**示例1:**  

	给定 nums = [-2, 0, 3, -5, 2, -1]，求和函数为 sumRange()

	sumRange(0, 2) -> 1
	sumRange(2, 5) -> -1
	sumRange(0, 5) -> -3


**说明：**

1. 你可以假设数组不可变。
2. 会多次调用 sumRange 方法。

### 考点

动态规划


### 代码
执行用时: **132ms**, 内存消耗: **17.2MB**

```
class NumArray:

    def __init__(self, nums: List[int]):
        
        self.len = len(nums)
        if self.len < 1:
            return None
        
        self.sum = [0] * self.len
        
        self.sum[0] = nums[0]
        i = 1
        
        for num in nums[1:]:
            self.sum[i] = self.sum[i-1] + num
            i += 1
           

    def sumRange(self, i: int, j: int) -> int:
        return self.sum[j] if i == 0 else self.sum[j] - self.sum[i-1]


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(i,j)
```
