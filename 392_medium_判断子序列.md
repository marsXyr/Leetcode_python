# Leetcode 392 判断子序列
***
### 题目描述
给定字符串 **s** 和 **t** ，判断 **s** 是否为 **t** 的子序列。

你可以认为 **s** 和 **t** 中仅包含英文小写字母。字符串 **t** 可能会很长（长度 ~= 500,000），而 **s** 是个短字符串（长度 <=100）。

字符串的一个子序列是原始字符串删除一些（也可以不删除）字符而不改变剩余字符相对位置形成的新字符串。（例如，`"ace"`是`"abcde"`的一个子序列，而`"aec"`不是）。


**示例1:**   

	s = "abc", t = "ahbgdc"
	返回 true.
	
**示例2:**   

	s = "axc", t = "ahbgdc"
	返回 false.

**后续挑战：** 
如果有大量输入的 S，称作S1, S2, ... , Sk 其中 k >= 10亿，你需要依次检查它们是否为 T 的子序列。在这种情况下，你会怎样改变代码？ 


### 考点

双指针

### 思路

双指针常规做法


### 代码1(双指针)
执行用时: **248ms**, 内存消耗: **18.4MB**

```
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        i, j = 0, 0
        ls, lt = len(s), len(t)
        while i < ls and j < lt:
            if s[i] == t[j]:
                i += 1
            j += 1
            
        return True if i == ls else False
```

### 代码2(双指针高级做法)

```
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
    	# 判断 s 是否为 t 的子序列。
    	b = iter(t)  # 迭代器
    	return all(((i in b) for i in s ))
```

### 代码3(调用函数str.find)

```
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        idx = 0
        for i in range(len(s)):
            tmp = t[idx:].find(s[i])
            if tmp == -1:
                return False
            idx = idx + tmp + 1
        return True
```