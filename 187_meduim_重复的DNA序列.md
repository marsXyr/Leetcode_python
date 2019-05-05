# Leetcode 187 重复的DNA序列
***
### 题目描述
所有 DNA 由一系列缩写为 A，C，G 和 T 的核苷酸组成，例如：“ACGAATTCCG”。在研究 DNA 时，识别 DNA 中的重复序列有时会对研究非常有帮助。

编写一个函数来查找 DNA 分子中所有出现超多一次的10个字母长的序列（子串）。


**示例:**

	输入: s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT"

	输出: ["AAAAACCCCC", "CCCCCAAAAA"]


### 考点

* 哈希表

### 思路   
依次遍历10个子字符串，如果出现在res中，则对应key的value +1,如果不出现，则创建key。返回res中value大于等于2的key。


### 代码
执行用时: **116ms**, 内存消耗: **26MB**。


```
class Solution:
    def findRepeatedDnaSequences(self, s: str) -> List[str]:
        res = {}
        for i in range(len(s)-9):
            subs = s[i:i+10]
            res[subs] = res.get(subs, 0) + 1
        return list([i for i in res.keys() if res[i] >= 2]) 
```
