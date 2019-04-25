# Leetcode 647 回文子串
***
### 题目描述
给定一个字符串，你的任务是计算这个字符串中有多少个回文子串。  

具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被计为是不同的子串。


**示例1:**   
	
	输入: "abc"
	输出: 3
	解释: 三个回文子串: "a", "b", "c".
	
**示例2:**   
	
	输入: "aaa"
	输出: 6
	说明: 6个回文子串: "a", "a", "a", "aa", "aa", "aaa".
    	
**注意：**  

* 输入的字符串长度不会超过1000。
	

### 考点

* 字符串


### 代码  
执行用时: **1504ms**, 内存消耗: **211.7MB** （直观做法，但是时间和空间复杂度都很高，能AC）

```
class Solution:
    def countSubstrings(self, s: str) -> int:
        subs = [s[i:i + x + 1] for x in range(len(s)) for i in range(len(s) - x)]
        count = 0
        for x in subs:
            if x == x[::-1]:
                count += 1
        return count                   
```

### Smart Solution (44ms)
  
这个是直接暴力计算的，技巧型做法。  
 
```
class Solution:
    def countSubstrings(self, s):
        """
        :type s: str
        :rtype: int
        """
        num = 0
        n, i = len(s), 0
        while i < n:
            j = i
            while j < n and s[j] == s[i]:
                j += 1
            d = j - i
            num += d * (d + 1) // 2
            il, ir = i - 1, j
            while il >= 0 and ir < n and s[il] == s[ir]:
                num += 1
                il, ir = il - 1, ir + 1
            i = j
        return num
```







	