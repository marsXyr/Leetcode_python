# Leetcode 面试题 59-I 滑动窗口的最大值

***
### 题目描述

给定一个数组 nums 和滑动窗口的大小 k，请找出所有滑动窗口里的最大值。

**示例1：**

	输入: nums = [1,3,-1,-3,5,3,6,7], 和 k = 3
	输出: [3,3,5,5,6,7] 
	解释: 
	
	  滑动窗口的位置                最大值
	---------------               -----
	[1  3  -1] -3  5  3  6  7       3
	 1 [3  -1  -3] 5  3  6  7       3
	 1  3 [-1  -3  5] 3  6  7       5
	 1  3  -1 [-3  5  3] 6  7       5
	 1  3  -1  -3 [5  3  6] 7       6
	 1  3  -1  -3  5 [3  6  7]      7


**说明：**

* `你可以假设 k 总是有效的，在输入数组不为空的情况下，1 ≤ k ≤ 输入数组的大小。`



**考点**

滑动窗口

### 代码
执行用时: **364ms**, 内存消耗: **34.5MB**

```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        if not nums: return []
        import numpy as np
        nums = np.array(nums)
        res = []
        for i in range(k, len(nums) + 1):
            res.append(int(nums[i-k: i].max()))
        return res
```

### 代码2
```
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        deque = [];result = [] # deque也可以用collection里的双端队列实现
        for i in range(0, len(nums)):
            while deque and nums[i]>nums[deque[-1]]: # 只存有可能成为最大值的数字的index进deque
                deque.pop()
            deque.append(i)
            while i-deque[0]>k-1: # 如果相距超过窗口k长度则弃掉
                deque.pop(0)
            if i >= k-1:
                result.append(nums[deque[0]]) # 这过程中始终保持deque[0]为最大值的index
        return result
```



