# Leetcode 22 括号生成
***
### 题目描述

给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且**有效的**括号组合。

例如，给出 n = 3，生成结果为：

**示例：**

	[
      "((()))",
      "(()())",
      "(())()",
      "()(())",
      "()()()"
    ]

### 考点

回溯


### 代码
执行用时: **52ms**, 内存消耗: **13MB**

```
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        res = []
        
        def back(left, right, part):
            if left == right and left == n:
                res.append(part)
            if left > n or left < right:
                return 
            back(left+1, right, part+'(')
            back(left, right+1, part+')')
            
        back(0, 0, "")
        return res
```


