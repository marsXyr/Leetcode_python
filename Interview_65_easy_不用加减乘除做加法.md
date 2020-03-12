# Leetcode 面试题 65 不用加减乘除做加法

***
### 题目描述

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

**示例1：**

	输入: a = 1, b = 1
	输出: 2


**说明：**

* `a, b 均可能是负数或 0`
* `结果不会溢出 32 位整数`



**考点**

位运算


### 代码
执行用时: **56ms**, 内存消耗: **13.5MB**

```
class Solution:
    def add(self, a: int, b: int) -> int:
        a &= 0xFFFFFFFF
        b &= 0xFFFFFFFF
        while b:
            carry = a & b
            a ^= b
            b = ((carry) << 1) & 0xFFFFFFFF
        return a if a < 0x80000000 else ~(a^0xFFFFFFFF)
```




