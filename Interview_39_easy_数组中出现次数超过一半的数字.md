# Leetcode 面试题 39 数组中出现次数超过一半的数字
***
### 题目描述

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

**示例：**

	输入: [1, 2, 3, 2, 2, 2, 5, 4, 2]
	输出: 2


**说明：**

* `1 <= 数组长度 <= 50000`


**考点**

技巧

**思路**

摩尔投票法，与`card`元素相等则`count + 1`,不等则`count - 1`，当`count`等于0时，将当前元素赋值给`card`.


### 代码
执行用时: **68ms**, 内存消耗: **15MB**

```
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        count, card = 1, nums[0]
        for num in nums[1:]:
            count = count + 1 if card == num else count - 1
            if count == 0:
                card = num
                count = 1
        return card
```







