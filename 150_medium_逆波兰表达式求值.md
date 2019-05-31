# Leetcode 150 逆波兰表达式求值
***
### 题目描述

根据逆波兰表示法，求表达式的值。

有效的运算符包括 `+, -, *, / `。每个运算对象可以是整数，也可以是另一个逆波兰表达式。

**说明：**   

* 整数除法只保留整数部分。
* 给定逆波兰表达式总是有效的。换句话说，表达式总会得出有效数值且不存在除数为 0 的情况。 

**示例1:**  

	输入: ["2", "1", "+", "3", "*"]
	输出: 9
	解释: ((2 + 1) * 3) = 9
	
**示例2:**  

	输入: ["4", "13", "5", "/", "+"]
	输出: 6
	解释: (4 + (13 / 5)) = 6
	
**示例3:**  

	输入: ["10", "6", "9", "3", "+", "-11", "*", "/", "*", "17", "+", "5", "+"]
	输出: 22
	解释: 
  	((10 * (6 / ((9 + 3) * -11))) + 17) + 5
	= ((10 * (6 / (12 * -11))) + 17) + 5
	= ((10 * (6 / -132)) + 17) + 5
	= ((10 * 0) + 17) + 5
	= (0 + 17) + 5
	= 17 + 5
	= 22


### 考点

栈


### 代码
执行用时: **60ms**, 内存消耗: **13MB**。

```
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        stack = []
        for token in tokens:
            if token == '+':
                num1 = stack.pop()
                num2 = stack.pop()
                stack.append(num1 + num2)
                continue
            if token == '-':
                num1 = stack.pop()
                num2 = stack.pop()
                stack.append(num2 - num1)
                continue
            if token == '*':
                num1 = stack.pop()
                num2 = stack.pop()
                stack.append(num1 * num2)
                continue
            if token == '/':
                num1 = stack.pop()
                num2 = stack.pop()
                num = num2 // num1
                if (num < 0) and (num2 % num1 != 0):
                    num += 1
                stack.append(num)
                continue
            stack.append(int(token))
        return stack.pop()
            
```



