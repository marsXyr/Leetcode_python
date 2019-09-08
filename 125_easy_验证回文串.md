# Leetcode 125 验证回文串
***
### 题目描述

给定一个字符串，验证它是否是回文串，只考虑字母和数字字符，可以忽略字母的大小写。

**说明：** 本题中，我们将空字符串定义为有效的回文串。

**示例1:**

	输入: "A man, a plan, a canal: Panama"
	输出: true
	
**示例2:**

	输入: "race a car"
	输出: false


### 考点

双指针


### 代码1
执行用时: **80ms**, 内存消耗: **14.1MB**

```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        if not s: return True
        left, right = 0, len(s) - 1
        while left <= right:
            while left <= right and not s[left].isalnum():
                left += 1
            while left <= right and not s[right].isalnum():
                right -= 1
            if left <= right and s[left].lower() != s[right].lower():
                return False
            left += 1
            right -= 1
        return True
```

### 代码2(简洁)

```
class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = ''.join(filter(str.isalnum, s)).lower()
        return s == s[::-1]
```

