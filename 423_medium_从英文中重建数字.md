# Leetcode 423 从英文中重建数字
***
### 题目描述

给定一个**非空**字符串，其中包含字母顺序打乱的英文单词表示的数字`0-9`。按升序输出原始的数字。

**示例1:**

	输入: "owoztneoer"
	输出: "012" (zeroonetwo)


**示例2：**

	输入: "fviefuro"
	输出: "45" (fourfive)

	
**说明：**

1. 输入只包含小写英文字母。
2. 输入保证合法并可以转换为原始的数字，这意味着像 "abc" 或 "zerone" 的输入是不允许的。
3. 输入字符串的长度小于 50,000。


### 考点

字符串


### 代码
执行用时: **36ms**, 内存消耗: **13.4MB**

```
class Solution:
    def originalDigits(self, s: str) -> str:
        n0 = s.count('z')
        n2 = s.count('w')
        n4 = s.count('u')
        n6 = s.count('x')
        n8 = s.count('g')
        n3 = s.count('t') - n2 - n8
        n5 = s.count('f') - n4
        n7 = s.count('s') - n6
        n1 = s.count('o') - n0 - n2 - n4
        n9 = s.count('i') - n5 - n6 - n8
        
        nList = (n0, n1, n2, n3, n4, n5, n6, n7, n8, n9)
        
        return "".join(str(i) * n for i, n in enumerate(nList))
```



