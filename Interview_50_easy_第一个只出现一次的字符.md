# Leetcode 面试题 50 第一个只出现一次的字符
***
### 题目描述

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。

**示例1:**    

	 s = "abaccdeff"
	 返回 "b"
	
**示例2:**    

	 s = "" 
	 返回 " "

	
**说明：**

* `0 <= s 的长度 <= 50000`


### 考点

哈希表

### 思路

用counts统计每个字符出现的次数，用sort存储字符出现的顺序


### 代码
执行用时: **172ms**, 内存消耗: **13.5MB**

```
class Solution:
    def firstUniqChar(self, s: str) -> str:
        counts, sort = dict(), []
        for i, c in enumerate(s):
            counts[c] = counts.get(c, 0) + 1
            if c not in sort: sort.append(c)
        for c in sort:
            if counts[c] == 1: return c
        return " "
```


