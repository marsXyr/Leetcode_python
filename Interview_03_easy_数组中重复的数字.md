# Leetcode 面试题 03 数组中重复的数字
***
### 题目描述

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。


**示例1：**    

	输入：
	[2, 3, 1, 0, 2, 5, 3]
	输出：2 或 3 


	
**说明：**

* `2 <= n <= 100000`


**考点**

哈希表


### 代码1
执行用时: **56ms**, 内存消耗: **23MB**

```
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        hashTable = dict()
        for num in nums:
            if num not in hashTable:
                hashTable[num] = 1
            return num
```

### 代码2
```
class Solution:
    def findRepeatNumber(self, nums: List[int]) -> int:
        for i, x in enumerate(nums):
            while x != i:
                if nums[x] = x: return x
                temp = x
                nums[i], nums[temp] = nums[temp], x
```





