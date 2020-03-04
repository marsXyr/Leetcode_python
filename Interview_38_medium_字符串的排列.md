# Leetcode 面试题 38 字符串的排列
***
### 题目描述

输入一个字符串，打印出该字符串中字符的所有排列。

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

**示例：**

	输入：s = "abc"
	输出：["abc","acb","bac","bca","cab","cba"]


**说明：**

* `1 <= s 的长度 <= 8`


**考点**

回溯


### 代码
执行用时: **432ms**, 内存消耗: **21.7MB**

```
class Solution:
    def permutation(self, s: str) -> List[str]:
        if len(s) == 1: return [s]
        
        res = set()
        def back(s, cur):
            if not s: res.add(cur)
            for i in range(len(s)):
                back(s[:i]+s[i+1:], cur+s[i])
        back(s, "")
        return list(res)
```







