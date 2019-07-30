# Leetcode 66 加一
***
### 题目描述
给定一个由**整数**组成的**非空**数组所表示的非负整数，在该数的基础上加一。

最高位数字存放在数组的首位， 数组中每个元素只存储一个数字。

你可以假设除了整数 0 之外，这个整数不会以零开头。

**示例1:**

	输入: [1,2,3]
	输出: [1,2,4]
	解释: 输入数组表示数字 123。
	
**示例2:**

	输入: [4,3,2,1]
	输出: [4,3,2,2]
	解释: 输入数组表示数字 4321。


### 考点

数组


### 代码
执行用时: **44ms**, 内存消耗: **13.7MB**

```
class Solution:
    def plusOne(self, digits: List[int]) -> List[int]:
        flag = 1
        for i in range(len(digits)-1, -1, -1):
            if digits[i] + flag <= 9:
                digits[i] += flag
                flag = 0
                break
            else:
                digits[i] = 0
                flag = 1
        return digits if flag == 0 else [1]+digits
```