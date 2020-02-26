# Leetcode 面试题 05 替换空格
***
### 题目描述

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

**示例1：**    

	输入：s = "We are happy."
	输出："We%20are%20happy."


	
**说明：**

* `0 <= s 的长度 <= 10000`


**考点**

字符串


### 代码1
执行用时: **36ms**, 内存消耗: **13.4MB**

```
class Solution:
    def replaceSpace(self, s: str) -> str:
        return '%20'.join(s.split(' '))
        # return s.replace(" ", "%20")      
```





