# Leetcode 541 反转字符串II
***
### 题目描述
给定一个字符串和一个整数 k，你需要对从字符串开头算起的每个 2k 个字符的前k个字符进行反转。如果剩余少于 k 个字符，则将剩余的所有全部反转。如果有小于 2k 但大于或等于 k 个字符，则反转前 k 个字符，并将剩余的字符保持原样。

**示例1:**  

	输入: s = "abcdefg", k = 2
	输出: "bacdfeg"


**注意：**

* 该字符串只包含小写的英文字母。
* 给定字符串的长度和 k 在[1, 10000]范围内。


### 考点

字符串


### 代码
执行用时: **48ms**, 内存消耗: **14MB**

```
class Solution:
    def reverseStr(self, s: str, k: int) -> str:
        res = ""
        for i in range(0, len(s), 2 * k):
            res += s[i:i+k][::-1] + s[i+k:i+2*k]
        return res
```

