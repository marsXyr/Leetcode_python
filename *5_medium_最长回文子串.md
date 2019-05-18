# Leetcode 5 最长回文子串
***
### 题目描述
给定一个字符串 `s`，找到 `s` 中最长的回文子串。你可以假设 `s` 的最大长度为 1000。


**示例1:**  

	输入: "babad"
	输出: "bab"
	注意: "aba" 也是一个有效答案。
	
**示例2:**  

	输入: "cbbd"
	输出: "bb"


### 考点

* 动态规划/技巧

### 思路  
创建一个`dp`数组，`dp[i][j] = 1` 表示`i...j`子串为回文串，`dp[i][j]=1`取决于`s[i]=s[j] and s[i+1][j-1]=1`, `s[i]!=s[j]` 则 `dp[i][j]=0`。首先找出两种基本情况即：`dp[i][i] = 1` 和 `dp[i][i+1] == s[i]s[i+1]`,然后从子串长度为3开始，依次前后各加一个字符，判断新子串是否为回文子串。  
动态规划还是比较浪费时间。下面还有两种方法供参考。


### 代码(动态规划)
执行用时: **4844ms**, 内存消耗: **21MB**。

```
class Solution:
    def longestPalindrome(self, s: str) -> str:
        ls = len(s)
        if ls < 2:
            return '' if ls == 0 else s
        dp = [[0] * ls for _ in range(ls)]
        start, end = 0, 0
        for i in range(ls-1):
            dp[i][i] = 1
            if s[i] == s[i+1]:
                dp[i][i+1] = 1
                start = i
                end = i + 1
        for l in range(3, ls+1):
            low = 0
            while low + l - 1 < ls:
                high = low + l - 1
                if s[low] == s[high] and dp[low+1][high-1]:
                    dp[low][high] = 1
                    start = low
                    end = high
                low += 1
        return s[start:end+1]            
```

### 代码(中心扩展方法, 执行用时: 1220ms, 内存消耗: 13MB)
**思路：**扫一遍字符串s，对于回文子串长为奇数的情况，求s[i]为轴对称中心的回文子串最长值；回文子串长偶数的情况，求s[i]s[i+i] 为中心的最长值。最后求最长。时间复杂度o(n^2)，因为扫一遍o(n)，中心扩展也是o(n)。注意数组越界和下标。
   
```
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        start = end = 0
        
        for i in range(len(s)):
            len1 = self.centerexpand(s, i, i)   #回文串长度为奇数，aba
            len2 = self.centerexpand(s, i, i+1)  #回文串长度为偶数，abba
            maxlen = max(len1, len2)
            if maxlen > end - start + 1:
                start = i - (maxlen - 1)//2
                end = i + maxlen//2
        return s[start: end+1]
                
    def centerexpand(self,s,l,r):
        while l >= 0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return r - l - 1
```

### 代码(Manacher,执行用时: 132ms, 内存消耗: 12.9MB)
**思路：**   参考  
[https://blog.csdn.net/dyx404514/article/details/42061017](https://blog.csdn.net/dyx404514/article/details/42061017)   
[https://segmentfault.com/a/1190000003914228](https://segmentfault.com/a/1190000003914228)

```
class Solution:
    def longestPalindrome(self,s):
        """
        :type s: str
        :rtype: str
        """
        s = '#'+'#'.join(s)+'#'   #例如'#a#b#a#'
        pos = maxright = 0
        RL = [0]*len(s)     #RL是回文串半径，如回文串长3，RL=1，回文串长5，RL=2
        maxcenter = 0        #记录最长回文中心序号
        
        for i in range(len(s)):
            if i<maxright:              #i在maxright左侧
                RL[i] = min(maxright-i, RL[pos*2-i] )
            else:                       #i在maxright右侧（含）
                RL[i] = 0
            while i-RL[i]-1>=0 and i+RL[i]+1<len(s) and s[i-RL[i]-1] == s[i+RL[i]+1]:
                RL[i] += 1              #继续扩展（RL[j]短的情况是不需要继续扩展的，但多扩展一次也就出循环了）
            if i+RL[i] > maxright:      #更新maxright和i
                maxright = RL[i] + i
                pos = i
            if RL[i] > RL[maxcenter]:    #更新maxcenter
                maxcenter = i
        return s[maxcenter-RL[maxcenter]:maxcenter+RL[maxcenter]+1].replace('#','')
```

