# Leetcode 670 最大交换
***
### 题目描述

给定一个非负整数，你**至多**可以交换一次数字中的任意两位。返回你能得到的最大值。


**示例1:**  

	输入: 2736
	输出: 7236
	解释: 交换数字2和数字7。
	
**示例2:**  

	输入: 9973
	输出: 9973
	解释: 不需要交换。
	
**注意：**  
 
1. 给定数字的范围是 [0, 10^8]


### 考点

数学

### 思路
我们注意到给定数字的范围是[0, 10^8]，也就是说最多9位，完全可以用暴力搜索计算。


### 代码
执行用时: **52ms**, 内存消耗: **13.2MB**。

```
class Solution:
    def maximumSwap(self, num: int) -> int:
        if num < 10:
            return num
        max_num = num        
        num = str(num)     
        for i in range(len(num)):
            for j in range(i+1, len(num)):
                new_num = num[:i]+num[j]+num[i+1:j]+num[i]+num[j+1:]
                if int(new_num) > max_num:
                    max_num = int(new_num)
        return max_num
```

### 代码(其他做法：执行用时：52ms)

```
class Solution:
    def maximumSwap(self, num: int) -> int:
        nums = list(str(num))
        nums2 = sorted(nums, reverse=True)
        if nums == nums2:
            return num
        else:
            for i in range(len(nums)):
                if nums[i] != nums2[i]:
                    j = -1-nums[::-1].index(nums2[i])
                    nums[i],nums[j] = nums[j],nums[i]
                    break
        return int(''.join(nums))
```
