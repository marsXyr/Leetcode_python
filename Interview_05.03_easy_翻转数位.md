# Leetcode 面试题 05.03 翻转数位
***
### 题目描述

给定一个32位整数 `num`，你可以将一个数位从0变为1。请编写一个程序，找出你能够获得的最长的一串1的长度。


**示例1:**    

	输入: num = 1775(110111011112)
	输出: 8
	
**示例2:**    

	输入: num = 7(01112)
	输出: 4


### 考点

位运算


### 代码
执行用时: **108ms**, 内存消耗: **28MB**

```
class Solution:
    def reverseBits(self, num: int) -> int:
        num2List = bin(num).split('0')
        res = -1
        for i in range(1, len(num2List)):
            res = max(res, num2List[i-1].count('1') + num2List[i].count('1') + 1)
        return res
```



