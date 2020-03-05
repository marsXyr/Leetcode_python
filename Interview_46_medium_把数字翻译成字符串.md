# Leetcode 面试题 46 把数字翻译成字符串
***
### 题目描述

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 
**示例1：**

	输入: 12258
	输出: 5
	解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
	
	

**说明：**

* `0 <= num < 2^31`


**考点**

动态规划


### 代码
执行用时: **40ms**, 内存消耗: **13.5MB**

```
class Solution:
    def translateNum(self, num: int) -> int:
        if num < 10: return 1
        num = str(num)
        dp = [0] * len(num)
        dp[0] = 1
        dp[1] = 2 if '10' <= num < '26' else 1
        
        for i in range(2, len(num)):
            dp[i] = dp[i-1]
            if '10' <= num[i-1:] < '26':
                dp[i] += dp[i-2]
        return dp[-1]
```






