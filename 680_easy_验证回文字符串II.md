# Leetcode 680 验证回文字符串II
***
### 题目描述

给定一个非空字符串 `s`，最多删除一个字符。判断是否能成为回文字符串。

**示例1:**

	输入: "aba"
	输出: True
	
**示例2:**

	输入: "abca"
	输出: True
	解释: 你可以删除c字符。


**注意：**

1. 字符串只包含从 `a-z` 的小写字母。字符串的最大长度是`50000`。


### 考点

字符串

### 思路

设置双指针`i = 0`, `j = Len(s) - 1`，只需要找到第一个`s[i] != s[j]`的位置，然后判断去掉`s[i]`或`s[j]`是否是回文串。


### 代码
执行用时: **168ms**, 内存消耗: **14.3MB**

```
class Solution:
    def validPalindrome(self, s: str) -> bool:
        L = len(s)
        i, j = 0, len(s) - 1
        
        def helper(ss):
            return True if ss == ss[::-1] else False
        
        while i <= j:
            if s[i] != s[j]:
                if not helper(s[i+1:j+1]) and not helper(s[i:j]):
                    return False
                else:
                    return True
            i += 1
            j -= 1
        return True
```
