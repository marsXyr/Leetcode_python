# Leetcode 415 字符串相加
***
### 题目描述
给定两个字符串形式的非负整数`num1`和`num2`，计算他们的和。  
    	
**注意：**  

1. num1 和num2 的长度都小于 5100.
2. num1 和num2 都只包含数字 0-9.
3. num1 和num2 都不包含任何前导零。
4. **你不能使用任何內建 BigInteger 库， 也不能直接将输入的字符串转换为整数形式。**
	

### 考点

* 字符串

### 思路
就暴力解呗。


### 代码  
执行用时: **84ms**, 内存消耗: **12.9MB** 

```
class Solution:
    def addStrings(self, num1: str, num2: str) -> str:
        l1, l2 = len(num1), len(num2)
        if l1 < l2: 
            num1, num2 = num2, num1
            l1, l2 = l2, l1
        num1, num2 = num1[::-1], num2[::-1]
        flag1, i = 0, 0
        while i < l2:
            add = int(num1[i]) + int(num2[i]) + flag1 
            if add > 9:
                add -= 10
                flag1 = 1
            else:
                flag1 = 0
            num1 = num1[:i]+str(add)+num1[i+1:]
            i += 1
        
        while i < l1:
            add = int(num1[i]) + flag1
            if add > 9:
                add -= 10
                flag1 = 1
            else:
                flag1 = 0
            num1 = num1[:i]+str(add)+num1[i+1:]
            i += 1
        if flag1 == 1:
            num1 += "1"
        return num1[::-1]
```






	