# Leetcode 334 递增的三元子序列
***
### 题目描述

给定一个未排序的数组，判断这个数组中是否存在长度为 3 的递增子序列。

数学表达式如下:
	
	如果存在这样的 i, j, k,  且满足 0 ≤ i < j < k ≤ n-1，
	使得 arr[i] < arr[j] < arr[k] ，返回 true ; 否则返回 false 。


**说明:** 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1) 。


**示例1:**  

	输入: [1,2,3,4,5]
	输出: true

**示例2:** 

	输入: [5,4,3,2,1]
	输出: false


### 考点

数组

### 思路

用`i`, `j`两个数分别记录遍历过的最小值和某一递增子序列的第二小的值，遍历`nums`数组过程中不断更新这两个数的值，如果遇到一个数`num`比这两个数都大，则说明存在一个递增的三元子序列。


### 代码
执行用时: **68ms**, 内存消耗: **14.3MB**

```
class Solution:
    def increasingTriplet(self, nums: List[int]) -> bool:
        i, j = float('inf'), float('inf')
        for num in nums:
            if num <= i:
                i = num
            elif num <= j:
                j = num
            else:
                return True
        return False
```
