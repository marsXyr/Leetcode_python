# Leetcode 171 Excel表列序号
***
### 题目描述

给定一个Excel表格中的列名称，返回其相应的列序号。

例如,

    A -> 1  
    B -> 2    
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 
    ...


**示例1:**  

	输入: "A"
	输出: 1

**示例2:**  

	输入: "AB"
	输出: 28
	
**示例3:**  

	输入: "ZY"
	输出: 701


### 考点

数学

### 代码
执行用时: **48ms**, 内存消耗: **13.1MB**。

```
class Solution:
    def titleToNumber(self, s: str) -> int:
        res = 0
        for c in s:
            res =  res * 26 + ord(c) - 64
        return res
```



