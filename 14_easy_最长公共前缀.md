# Leetcode 14 最长公共前缀
***
### 题目描述
编写一个函数来查找字符串数组中的最长公共前缀。

如果不存在公共前缀，返回空字符串 `""`。

**示例1：**

	输入: ["flower","flow","flight"]
	输出: "fl"
	
**示例2：**

	输入: ["dog","racecar","car"]
	输出: ""
	解释: 输入不存在公共前缀。
	
**提示：**

* 所有输入只包含小写字母 `a-z`。 

### 考点

字符串


### 代码
执行用时: **56ms**, 内存消耗: **13.1MB**

```
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        l = len(strs)
        if l == 0:
            return ""
        res = ""
        based = strs[0]
        for i in range(len(based)):
            for str_ in strs[1:]:
                if len(str_) <= i or based[i] != str_[i]:
                    return res
            res += based[i]
        return res
```

### 代码2(执行用时：40ms)

```
class Solution:
    def longestCommonPrefix(self, strs: List[str]) -> str:
        if len(strs) == 0:
            return ""
        s1 = min(strs)
        s2 = max(strs)
        for j,k in enumerate (s1):
            if k != s2[j]:
                return s2[:j]
        return s1
```