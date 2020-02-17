# Leetcode 525 连续数组
***
### 题目描述

给定一个二进制数组, 找到含有相同数量的 0 和 1 的最长连续子数组（的长度）。


**示例1:**

	输入: [0,1]
	输出: 2
	说明: [0, 1] 是具有相同数量0和1的最长连续子数组。


**示例2：**

	输入: [0,1,0]
	输出: 2
	说明: [0, 1] (或 [1, 0]) 是具有相同数量0和1的最长连续子数组。
	
**说明：**

*  给定的二进制数组的长度不会超过50000。


### 考点

哈希表

### 思路

1. 将所有的0转化为-1，问题转化为和为0的最长连续子数组。
2. 用哈希表记录前缀和第一次出现的位置。
3. 遍历数组，找到最后一次出现在哈希表中前缀和的位置。

(注意：哈希表中初始化前缀和为0的值为0)


### 代码
执行用时: **1028ms**, 内存消耗: **17.6MB**

```
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        hashMap = dict()
        hashMap[0] = 0
        curSum = 0
        res = 0
        for i, num in enumerate(nums):
            curSum = curSum + 1 if num == 1 else curSum - 1
            if curSum in hashMap:
                res = max(res, i + 1 - hashMap[curSum])
            else:
                hashMap[curSum] = i + 1        
        return res
```



