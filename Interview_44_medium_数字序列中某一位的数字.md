# Leetcode 面试题 44 数字序列中某一位的数字
***
### 题目描述

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

**示例1：**

	输入：n = 3
	输出：3
	
**示例2：**

	输入：n = 11
	输出：0


**说明：**

* `0 <= n < 2^31`


**考点**

数学


### 代码
执行用时: **56ms**, 内存消耗: **13.2MB**

```
class Solution:
    def findNthDigit(self, n: int) -> int:
        base = 9
        digits = 1
        while n - base * digits > 0:
            n -= base * digits
            base *= 10
            digits += 1

        idx = n % digits
        if idx == 0:
            idx = digits
        number = 10 ** (digits-1)

        if idx == digits:
            number += n // digits - 1
        else:
            number += n // digits
        
        for i in range(idx, digits):
            number //= 10
        
        return number % 10
```







