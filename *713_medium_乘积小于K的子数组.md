# Leetcode 713 乘积小于K的子数组
***
### 题目描述

给定一个正整数数组 `nums`。

找出该数组内乘积小于 `k` 的连续的子数组的个数。


**示例1:**  

	输入: nums = [10,5,2,6], k = 100
	输出: 8
	解释: 8个乘积小于100的子数组分别为: [10], [5], [2], [6], [10,5], [5,2], [2,6], [5,2,6]。
	需要注意的是 [10,5,2] 并不是乘积小于100的子数组。
	
	
**提示：**  
 
1. `0 < nums.length <= 50000`
2. `0 < nums[i] < 1000`
3. `0 <= k < 10^6`


### 考点

双指针

### 思路
技巧解法。只需遍历一遍数组。prod记录当前乘积值，如果大于K，则除以起始端的值。每循环一次，结果加上本次合法的乘积个数。


### 代码
执行用时: **404ms**, 内存消耗: **15.6MB**。

```
class Solution:
    def numSubarrayProductLessThanK(self, nums: List[int], k: int) -> int:
        i = 0
        prod = 1
        res = 0
        for j in range(len(nums)):
            prod *= nums[j]
            while j >= i and prod >= k:
                prod /= nums[i]
                i += 1
            res += j-i+1
        return res
```
