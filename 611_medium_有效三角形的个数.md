# Leetcode 611 有效三角形的个数
***
### 题目描述

给定一个包含非负整数的数组，你的任务是统计其中可以组成三角形三条边的三元组个数。


**示例1:**  

	输入: [2,2,3,4]
	输出: 3
	解释:
	有效的组合是: 
	2,3,4 (使用第一个 2)
	2,3,4 (使用第二个 2)
	2,2,3

**注意:**  

1.	数组长度不超过1000。
2. 数组里整数的范围为 [0, 1000]。


### 考点

数组


### 代码
执行用时: **284ms**, 内存消耗: **13.9MB**

```
class Solution:
    def triangleNumber(self, nums: List[int]) -> int:
        nums.sort()
        res = 0
        # 从大到小遍历
        for i in range(len(nums) - 1, 1, -1):
            l, r = 0, i - 1
            while l < r:
                # 如果下标l, r, i能组成三角形，则l...r下标都能组成
                if nums[l] + nums[r] > nums[i]:
                    # 个数为 r - l
                    res += r - l
                    r -= 1
                else:
                    l += 1       
        return res
```
