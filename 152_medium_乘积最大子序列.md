# Leetcode 152 乘积最大子序列
***
### 题目描述
给定一个整数数组`nums`，找出一个序列中乘积最大的连续子序列（该序列至少包含一个数）。   


**示例1:**   
	
	输入: [2,3,-2,4]
	输出: 6  
	解释: 子数组 [2,3] 有最大乘积6。

**示例2:**   
	
	输入: [-2,0,-1]
	输出: 0  
	解释: 结果不能为2，因为 [-2,-1] 不是子数组。

### 考点

* 动态规划


### 思路 
设置两个值最大正数积和最小负数积，遍历数组，动态规划计算当前位置的最大正数积和最小负数积，然后与当前位置做比较。 

### 代码  
执行用时 **104ms**, 内存消耗 **13.4MB**

```
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        if len(nums) == 1: return nums[0]
        pmax, nmin = 0, 0
        res = nums[0]
        for x in nums:
            tmp = pmax
            pmax = max(x, max(x * pmax, x * nmin))
            nmin = min(x, min(x * tmp, x * nmin))
            res = max(pmax, res)
        return res              
```

### Smart Solution
计算从左到右相乘的最大值，再计算从右到左的最大值；再将两组最大值相比。

```
class Solution:
    def maxProduct(self, A):
        B = A[::-1]
        for i in range(1, len(A)):
            A[i] *= A[i - 1] or 1
            B[i] *= B[i - 1] or 1
        return max(max(A),max(B))
```




	
