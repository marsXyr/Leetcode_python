# Leetcode 300 最长上升子序列
***
### 题目描述

给定一个无序的整数数组，找到其中最长上升子序列的长度。

**示例:**  

	输入: [10,9,2,5,3,7,101,18]
	输出: 4 
	解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。

**说明：**   

* 可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
* 你算法的时间复杂度应该为 O(n^2) 。

**进阶：** 你能将算法的时间复杂度降低到 O(nlogn) 吗?

### 考点

动态规划

### 思路

`O(n^2)`代码思路很简单，就是对每个遍历到的元素`nums[i]`，找 `0...i` 范围内比`nums[i]`小的最大的元素的最长子序列的长度然后`+1`。

### 代码1(动态规划)
执行用时: **1440ms**, 内存消耗: **13.2MB**。

```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        l = len(nums)
        if l <= 1:
            return l
        dp = [1] * l
        for i in range(l):
            for j in range(i):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j] + 1)
        return max(dp)
```

### 代码2(二分查找, 执行用时：52ms)

```

class Solution:
    def lengthOfLIS(self, nums: 'List[int]') -> 'int':
        if not nums:
            return 0
        res=[nums[0]]
        for i in range(1,len(nums)):
            if nums[i]>res[-1]:
                res.append(nums[i])
            else:
                left,right=0,len(res)-1
                while left<=right:
                    mid=(left+right)//2
                    if nums[i]>res[mid]:
                        left=mid+1
                    else:
                        right=mid-1
                res[left]=nums[i]
        return len(res)
```


### 代码3(大佬做法, 执行用时：36ms)

```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        temp = []
        for n in nums:
	if not temp or n > temp[-1]:
	    temp.append(n)
	else:
	    temp[bisect.bisect_left(temp, n)] = n
        return len(temp)
```


