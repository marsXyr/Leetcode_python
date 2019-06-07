# Leetcode 557 反转字符串中的单词III
***
### 题目描述

给定一个字符串，你需要反转字符串中每个单词的字符顺序，同时仍保留空格和单词的初始顺序。

**示例1：**

	输入: "Let's take LeetCode contest"
	输出: "s'teL ekat edoCteeL tsetnoc" 

**注意：** 在字符串中，每个单词由单个空格分隔，并且字符串中不会有任何额外的空格。

### 考点

字符串

### 代码
执行用时: **52ms**, 内存消耗: **13.2MB**。

```
class Solution:
    def reverseWords(self, s: str) -> str:
        ls = s.split()
        for i, s in enumerate(ls):
            ls[i] = s[::-1]
        return ' '.join(ls)
        
        # return ' '.join(i[::-1] for i in s.split())
```





