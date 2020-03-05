# Leetcode 面试题 48 最长不含重复字符的子字符串
***
### 题目描述

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

**示例1：**

	输入: "abcabcbb"
	输出: 3 
	解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。

**示例2：**

	输入: "bbbbb"
	输出: 1
	解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
	
**示例3：**

	输入: "pwwkew"
	输出: 3
	解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
	请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。	
	

**说明：**

* `s.length <= 40000`


**考点**

滑动窗口、双指针


### 代码
执行用时: **80ms**, 内存消耗: **13.5MB**

```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        if not s: return 0        
        ws = s[0]
        res = 1
        for i in range(1, len(s)):
            if s[i] not in ws:
                ws += s[i]
                res = max(res, len(ws))
            else:
                for j in range(len(ws)):
                    if ws[j] == s[i]: break
                ws = ws[j+1:] + s[i]
        return res
```

### 优化后的代码
```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        
        res, head = 0, 0
        hashMap = {}
        for tail in range(len(s)):
            if s[tail] in hashMap:
                head = max(head, hashMap[s[tail]])
            hashMap[s[tail]] = tail + 1
            res = max(res, tail - head + 1)
        return res
```





