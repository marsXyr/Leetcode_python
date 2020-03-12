# Leetcode 面试题 64 求1+2+...+n

***
### 题目描述

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

**示例1：**

	输入: n = 3
	输出: 6


**示例2：**

	输入: n = 9
	输出: 45


**说明：**

* `1 <= n <= 10000`



**考点**

递归


### 代码
执行用时: **44ms**, 内存消耗: **21.1MB**

```
class Solution:
    def sumNums(self, n: int) -> int:
        return n and n + self.sumNums(n-1)
```




