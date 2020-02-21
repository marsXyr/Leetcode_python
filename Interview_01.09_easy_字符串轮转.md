# Leetcode 面试题 01.09 字符串轮转
***
### 题目描述

字符串轮转。给定两个字符串`s1`和`s2`，请编写代码检查`s2`是否为`s1`旋转而成（比如，`waterbottle`是`erbottlewat`旋转后的字符串）。

**示例1:**    

	输入：s1 = "waterbottle", s2 = "erbottlewat"
	输出：True
	
**示例2:**    

	输入：s1 = "aa", "aba"
	输出：False
	
**提示：**

* 字符串长度在[0, 100000]范围内。


### 考点

字符串


### 代码
执行用时: **108ms**, 内存消耗: **28MB**

```
class Solution:
    def isFlipedString(self, s1: str, s2: str) -> bool:
        return len(s1) == len(s2) and (s1 in s2+s2)
```



