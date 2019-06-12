# Leetcode 49 字母异位词分组
***
### 题目描述

给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。

**示例1：**

	输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
	输出:
	[
      ["ate","eat","tea"],
      ["nat","tan"],
      ["bat"]
    ]


**说明：**

* 所有输入均为小写字母。
* 不考虑答案输出的顺序。
	


### 考点

哈希表

### 思路
常规做法，用字典存放字母异位词，键为排序后的字母异位词。

### 代码
执行用时: **196ms**, 内存消耗: **15.5MB**。

```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        res = []
        dic = {}
        for s in strs:
            keys = "".join(sorted(s))
            if keys not in dic:
                dic[keys] = [s]
            else:
                dic[keys].append(s)
        return list(dic.values())
```

### 代码2(大佬做法, 执行用时: 128ms)

```
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        hashmap = collections.defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord('a')] += 1
            hashmap[tuple(count)].append(s)
        return list(hashmap.values())
```




