# Leetcode 290 单词规律
***
### 题目描述

给定一种规律 `pattern` 和一个字符串 `str` ，判断 `str` 是否遵循相同的规律。

这里的 **遵循** 指完全匹配，例如， `pattern` 里的每个字母和字符串 `str` 中的每个非空单词之间存在着双向连接的对应规律。

**示例1：**

	输入: pattern = "abba", str = "dog cat cat dog"
	输出: true

**示例2：**

	输入:pattern = "abba", str = "dog cat cat fish"
	输出: false

**示例3：**

	输入: pattern = "aaaa", str = "dog cat cat dog"
	输出: false
	
**示例4：**

	输入: pattern = "abba", str = "dog dog dog dog"
	输出: false

**说明：**  

你可以假设 `pattern` 只包含小写字母， `str` 包含了由单个空格分隔的小写字母。

### 考点

哈希表


### 代码
执行用时: **44ms**, 内存消耗: **13MB**。

```
class Solution:
    def wordPattern(self, pattern: str, str: str) -> bool:
        list_str = str.split()
        if len(list_str) != len(pattern) or len(set(list_str)) != len(set(pattern)):
            return False
        dic = {}
        for i, p in enumerate(pattern):
            if p not in dic:
                dic[p] = list_str[i]
            else:
                if dic[p] != list_str[i]:
                    return False
        return True
```





