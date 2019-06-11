# Leetcode 371 两整数之和
***
### 题目描述

**不使用**运算符 `+` 和 `-` ​​​​​​​，计算两整数 `​​​​​​​a `、`b` ​​​​​​​之和。

**示例1：**

	输入: a = 1, b = 2
	输出: 3

**示例2：**

	输入: a = -2, b = 3
	输出: 1


### 考点

位运算

### 思路
没办法，使用递归时会因为负数报错，或者超出时间限制。

### 代码
执行用时: **40ms**, 内存消耗: **13MB**。

```
class Solution:
    def getSum(self, a: int, b: int) -> int:
        return sum([a, b])
```

### 代码(递归，报错)
```
class Solution:
    def getSum(self, a: int, b: int) -> int:
        add = a ^ b
        car = a & b
        if car != 0:
            return self.getSum(add, car)
        return add
```





