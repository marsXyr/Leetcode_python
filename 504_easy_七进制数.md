# Leetcode 504 七进制数
***
### 题目描述

给定一个整数，将其转化为7进制，并以字符串形式输出。

**示例1：**

	输入: 100
	输出: "202"

**示例2：**

	输入: -7
	输出: "-10"


**注意：** 输入范围是 [-1e7, 1e7] 。

### 考点

数学

### 代码
执行用时: **44ms**, 内存消耗: **13MB**。

```
class Solution:
    def convertToBase7(self, num: int) -> str:
        if num == 0:
            return "0"
        flag = 1 if num > 0 else -1
        res = ""
        while num != 0:
            res = str(abs(num) % 7) + res
            num = abs(num) // 7
        return res if flag == 1 else '-'+res
```





