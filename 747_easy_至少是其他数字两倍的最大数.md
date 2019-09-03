# Leetcode 747 至少是其他数字两倍的最大数
***
### 题目描述

在一个给定的数组`nums`中，总是存在一个最大元素 。

查找数组中的最大元素是否至少是数组中每个其他数字的两倍。

如果是，则返回最大元素的索引，否则返回-1。


**示例1:**

	输入: nums = [3, 6, 1, 0]
	输出: 1
	解释: 6是最大的整数, 对于数组中的其他整数,
	6大于数组中其他元素的两倍。6的索引是1, 所以我们返回1.
	
**示例2:**

	输入: nums = [1, 2, 3, 4]
	输出: -1
	解释: 4没有超过3的两倍大, 所以我们返回 -1.


**提示：**

1. `nums` 的长度范围在`[1, 50]`.
2. 每个 `nums[i]` 的整数范围在 `[0, 99]`.


### 考点

数组


### 思路

因为数组`nums`长度小，所以暴力求解跟其他方法没什么区别。


### 代码
执行用时: **48ms**, 内存消耗: **13.9MB**

```
class Solution:
    def dominantIndex(self, nums: List[int]) -> int:
        maxNum = max(nums)
        idxMax = nums.index(maxNum)
        for i, num in enumerate(nums):
            if maxNum < 2 * num and i != idxMax:
                return -1
        return idxMax
```
