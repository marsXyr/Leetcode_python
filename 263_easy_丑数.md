# Leetcode 263 丑数
***
### 题目描述

编写一个程序判断给定的数是否为丑数。

丑数就是只包含质因数 `2, 3, 5` 的**正整数**。


**示例1:**  

	输入: 6
	输出: true
	解释: 6 = 2 × 3
	
**示例2:**  

	输入: 8
	输出: true
	解释: 8 = 2 × 2 × 2
	
**示例3:**  

	输入: 14
	输出: false 
	解释: 14 不是丑数，因为它包含了另外一个质因数 7。
	
**提示：**  
 
1. `1` 是丑数。
2. 输入不会超过 32 位有符号整数的范围: [−231,  231 − 1]。


### 考点

数学


### 代码
执行用时: **48ms**, 内存消耗: **13.1MB**。

```
class Solution:
    def isUgly(self, num: int) -> bool:
        if num < 1:
            return False
        while True:
            if num % 2 == 0: num = num // 2
            if num % 3 == 0: num = num // 3
            if num % 5 == 0: num = num // 5
            if num % 2 != 0 and num % 3 != 0 and num % 5 != 0: break
        return True if num == 1 else False
```
