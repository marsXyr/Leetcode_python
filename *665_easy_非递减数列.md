# Leetcode 665 非递减数列
***
### 题目描述
给定一个长度为 `n` 的整数数组，你的任务是判断在**最多**改变 `1` 个元素的情况下，该数组能否变成一个非递减数列。

我们是这样定义一个非递减数列的： 对于数组中所有的 `i` (1 <= i < n)，满足 `array[i] <= array[i + 1]`。

**示例1:**

	输入: [4,2,3]
	输出: True
	解释: 你可以通过把第一个4变成1来使得它成为一个非递减数列。

**示例2:**

	输入: [4,2,1]
	输出: False
	解释: 你不能在只改变一个元素的情况下将其变为非递减数列。
	
**说明：**  
`n` 的范围为 [1, 10,000]。

### 考点

* 数组

### 思路   
先让前两个有序。如果出现 nums[i] > nums[i+1]，则需要改变一个数，此时面临两种选择：1.把nums[i]变大，2.把nums[i+1]变小。至于怎么选择，取决于nums[i-1]与nums[i+1]值的大小。eg:... 1 4 3 ...只能选择把4变小, ... 3 4 1 ...只能选择把1变大。改变完后次数+1。如果次数大于1，就立即返回。


### 代码
执行用时: **68ms**, 内存消耗: **14.1MB**。


```
class Solution:
    def checkPossibility(self, nums: List[int]) -> bool:
        l = len(nums)
        if l < 2:
            return True
        count = 0
        if nums[0] > nums[1]:
            nums[0] = nums[1]
            count += 1
        
        for i in range(1, l-1):
            if nums[i] > nums[i+1]:
                count += 1
                if count >= 2:
                    return False
                if nums[i+1] < nums[i-1]:
                    nums[i+1] = nums[i]
                else:
                    nums[i] = nums[i-1]
                           
        return True           
```
