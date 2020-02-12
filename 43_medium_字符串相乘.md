# Leetcode 43 字符串相乘
***
### 题目描述

给定两个以字符串形式表示的非负整数 `num1` 和 `num2`，返回 `num1` 和 `num2` 的乘积，它们的乘积也表示为字符串形式。


**示例1:**

	输入: num1 = "2", num2 = "3"
	输出: "6"


**示例2：**

	输入: num1 = "123", num2 = "456"
	输出: "56088"
	

**说明：**

* `num1` 和 `num2` 的长度小于110。
* `num1` 和 `num2` 只包含数字 `0-9`。
* `num1` 和 `num2` 均不以零开头，除非是数字 0 本身。
* 不能使用任何标准库的大数类型（比如 BigInteger）或直接将输入转换为整数来处理。

### 考点

字符串


### 代码
执行用时: **120ms**, 内存消耗: **13.2MB**

```
class Solution:
    def multiply(self, num1: str, num2: str) -> str:
        res = 0       
        for s2 in num2:
            temp = 0
            for s1 in num1:
                temp = temp * 10 + int(s1) * int(s2)
            res = res * 10 + temp
        return str(res)
```



