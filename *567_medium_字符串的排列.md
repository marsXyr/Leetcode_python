# Leetcode 567 字符串的排列
***
### 题目描述
给定两个字符串 **s1** 和 **s2**，写一个函数来判断 **s2** 是否包含 **s1** 的排列。

换句话说，第一个字符串的排列之一是第二个字符串的子串。


**示例1：**

	输入: s1 = "ab" s2 = "eidbaooo"
	输出: True
	解释: s2 包含 s1 的排列之一 ("ba").


**示例2：**

	输入: s1= "ab" s2 = "eidboaoo"
	输出: False


**注意：**

1.  输入的字符串只包含小写字母
2. 两个字符串的长度都在 [1, 10,000] 之间


### 考点

双指针，滑动窗口


### 思路

用两个哈希表`dict1`, `dict2`分别存储`s1`各字符的数量及`s2`各字符的数量，用一个`size`为`s1`长度的滑动窗口遍历`s2`，如果某刻两个哈希表完全一样，则说明存在。


### 代码(暴力统计窗口内字符数量)
执行用时: **2680ms**, 内存消耗: **13.1MB**

```
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        from collections import Counter
        ls1, ls2 = len(s1), len(s2)
        left, right = 0, ls1
        cs1 = Counter(s1)
        while right <= ls2:
            if Counter(s2[left:right]) == cs1:
                return True
            else:
                left += 1
                right += 1               
        return False
```

### 代码2(优化后，执行用时72ms):

```
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        l1=len(s1)
        l2=len(s2)
        if l2<l1:
            return False
        s='abcdefghijklmnopqrstuvwxyz'
        dict1={}
        dict2={}
        for char in s:
            dict1[char]=0
            dict2[char]=0
        for i in range(l1):
            dict1[s1[i]]+=1
            dict2[s2[i]]+=1       
        if dict1 == dict2:
            return True
        for i in range(l2-l1):
            dict2[s2[i]]-=1
            dict2[s2[i+l1]]+=1
            if dict1 == dict2:
                return True
        return False
```
