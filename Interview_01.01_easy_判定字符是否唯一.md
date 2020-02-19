# Leetcode 面试题 01.01 判定字符是否唯一
***
### 题目描述

实现一个算法，确定一个字符串 s 的所有字符是否全都不同。


**示例1:**

	输入: s = "leetcode"
	输出: false 

**示例2:**

	输入: s = "abc"
	输出: true


**提示：**

* `0 <= len(s) <= 100`
* 如果你不使用额外的数据结构，会很加分。


### 考点

字符串


### 代码
执行用时: **240ms**, 内存消耗: **13.6MB**

```
class Solution:
    def isUnique(self, astr: str) -> bool:
        for i in range(len(astr)):
            res_astr = astr[:i] + astr[i+1:]
            if astr[i] in res_astr:
                return False
        return True
```



