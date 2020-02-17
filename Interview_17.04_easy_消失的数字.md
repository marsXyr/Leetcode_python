# Leetcode 面试题 17.04 消失的数字
***
### 题目描述

数组nums包含从0到n的所有整数，但其中缺了一个。请编写代码找出那个缺失的整数。你有办法在O(n)时间内完成吗？


**示例1:**

	输入：[3,0,1]
	输出：2


**示例2：**

	输入：[9,6,4,2,3,5,7,0,1]
	输出：8


### 考点

数学


### 代码
执行用时: **148ms**, 内存消耗: **14MB**

```
class Solution:
    def missingNumber(self, nums: List[int]) -> int:
        l = len(nums)
        return l * (l + 1) // 2 - sum(nums)
```



