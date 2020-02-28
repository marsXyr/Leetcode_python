# Leetcode 面试题 21 调整数组顺序使奇数位于偶数前面
***
### 题目描述

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

**示例1：**    

	输入：nums = [1,2,3,4]
	输出：[1,3,2,4] 
	注：[3,1,2,4] 也是正确的答案之一。
	
	
**说明：**

* `1 <= nums.length <= 50000`
* `1 <= nums[i] <= 10000`


**考点**

数组


### 代码
执行用时: **48ms**, 内存消耗: **17.8MB**

```
class Solution:
    def exchange(self, nums: List[int]) -> List[int]:
        i, right = 0, len(nums) - 1
        while i < right:
            if nums[i] % 2 == 0:
                while i < right and nums[right] % 2 == 0:
                    right -= 1
                nums[i], nums[right] = nums[right], nums[i]
                right -= 1
            i += 1
        return nums
```

### 代码2（一行）

```
class Solution:
    def exchange(self, nums: List[int]) -> List[int]:        
        return sorted(nums,key=lambda x:1-x%2)
```








