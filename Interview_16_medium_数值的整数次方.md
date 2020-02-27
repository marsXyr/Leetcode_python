# Leetcode 面试题 16 数值的整数次方
***
### 题目描述

实现函数double Power(double base, int exponent)，求base的exponent次方。不得使用库函数，同时不需要考虑大数问题。


**示例1：**    

	输入: 2.00000, 10
	输出: 1024.00000
	
**示例2：**

	输入: 2.10000, 3
	输出: 9.26100

**示例3：**

	输入: 2.00000, -2
	输出: 0.25000
	解释: 2-2 = 1/22 = 1/4 = 0.25

**说明：**

* `-100.0 < x < 100.0`
* `n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。`


**考点**

递归


### 代码
执行用时: **36ms**, 内存消耗: **13.5MB**

```
class Solution:
    def myPow(self, x: float, n: int) -> float:
        
        def helper(x, n):
            if n == 1: return x
            elif n & 1: return x * helper(x, n-1)
            else: return helper(x * x, n // 2)
            
        if n > 0: return helper(x, n)
        elif n == 0: return 1.0
        else: return helper(1.0 / x, -n)
```








