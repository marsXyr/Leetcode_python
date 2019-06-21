# Leetcode 3 无重复字符的最长子串
***
### 题目描述

给定一个字符串，请你找出其中不含有重复字符的 **最长子串** 的长度。

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
	

### 考点

滑动窗口/哈希表/双指针

### 思路
我是采用滑动窗口/双指针方法做的。  
左窗口left，右窗口right，如果窗口内的字符串元素互不相同则右窗口右移一位，否则左右窗口同时右移一位。遍历结束时窗口的大小即为无重复字符的最长子串(因为窗口大小只增不减)。

### 代码
执行用时: **224ms**, 内存消耗: **13MB**

```
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        left, right = 0, 0
        while right < len(s):
            if len(s[left:right+1]) != len(set(s[left:right+1])):
                left += 1
            right += 1
        return right - left
```

### 代码2(其他做法，执行用时：56ms)

```
class Solution:
    def lengthOfLongestSubstring(self, s):
        dicts = {}
        maxlength = start = 0
        for i,value in enumerate(s):
            if value in dicts:
                sums = dicts[value] + 1
                if sums > start:
                    start = sums
            num = i - start + 1
            if num > maxlength:
                maxlength = num
            dicts[value] = i
        return maxlength
```

