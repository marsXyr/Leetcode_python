# Leetcode 面试题 61 扑克牌中的顺子

***
### 题目描述

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。


**示例1：**

	输入: [1,2,3,4,5]
	输出: True

**示例2：**

	输入: [0,0,1,2,5]
	输出: True


**说明：**

* `数组长度为 5 `
* `数组的数取值为 [0, 13] .`



**考点**

数组

### 代码
执行用时: **48ms**, 内存消耗: **13.4MB**

```
class Solution:
    def isStraight(self, nums: List[int]) -> bool:
        
        nums = sorted(nums)
        zeros = 0
        for i in range(4):
            if nums[i] == 0:
                zeros += 1
                continue
            if nums[i] == nums[i+1]:
                return False
            else:
                zeros -= nums[i+1] - nums[i] - 1
        return False if zeros < 0 else True
```



