# Leetcode 50 Pow(x,n)
***
### 题目描述

实现 `pow(x, n)` ，即计算 `x` 的 `n` 次幂函数。

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

* -100.0 < x < 100.0
* n 是 32 位有符号整数，其数值范围是 [−231, 231 − 1] 。


### 考点

二分查找


### 代码
执行用时: **48ms**, 内存消耗: **13.2MB**

```
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n == 0: return 1
        if n == 1: return x
        if n == -1: return 1/x
        flag = 1 if n > 0 else 0
        p = []
        n = abs(n)
        while n > 1:
            if n % 2 == 0 :
                p.append(2)
                n = n // 2
            else:
                p.append(1)
                n -= 1
        res = x
        for a in p[::-1]:
            if a == 1:
                res *= x
            else:
                res *= res
        return res if flag == 1 else 1/res
```

### 代码2(执行用时: 36ms)

```
class Solution:
    def myPow(self, x: float, n: int) -> float:
        if n < 0:
            x = 1/x
            n = -n
        pow = 1
        while n:
            if n & 1: #如果余数为1
                pow *= x
            x *= x
            n >>= 1
        return pow
```


